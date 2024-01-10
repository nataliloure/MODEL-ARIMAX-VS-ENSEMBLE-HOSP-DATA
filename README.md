# MODELO-ARIMAX-DADOSHOSP
Modelo Arimax para dados de óbitos hospitalares 

````

install.packages(c("forecast", "caret", "xgboost", "randomForest", "readxl", "modeltools", "tidyverse", "plotly", "ggplotly", "ggplot2", "tsibble"))

library(forecast)
library(caret)
library(xgboost)
library(randomForest)
library(readxl)
library(modeltools)
library(stats19)
library(stats4teaching)
library(statsr)
library(ggplotify)
library(tidyverse)
library(plotly)
library(ggplot2)
library(tsibble)


caminho_do_arquivo <- ""      

dados <- read_xlsx(caminho_do_arquivo) %>%
  mutate(ds = as.Date(ds, format = "%Y-%m-%d")) %>%
  as_tsibble(index = ds)

dados <- filter(dados, !is.na(ds) & ds >= as.Date("2012-01-01") & ds <= as.Date("2022-12-31"))

class(dados)
str(dados)

dados$ds <- as.Date(dados$ds, format = "%Y-%m-%d")
dados <- subset(dados, !is.na(ds) & ds >= as.Date("2012-01-01") & ds <= as.Date("2022-12-31"))
numero_de_passos_a_prever <- 12


dados_treino <- dados[1:(nrow(dados) - numero_de_passos_a_prever), ]
dados_teste <- dados[(nrow(dados) - numero_de_passos_a_prever + 1):nrow(dados), ]
str(dados_treino)
str(dados_teste)
ts_dados <- ts(dados_treino$numero_obitos, start = c(2012, 1), frequency = 12)
modelo_arimax <- auto.arima(ts_dados, xreg = dados_treino$dias_internacao)
plot(modelo_arimax)
checkresiduals(modelo_arimax)
summary(modelo_arimax)
previsoes <- forecast(modelo_arimax, xreg = dados$dias_internacao, h = 12)
plot(ts_dados, main = "Previsões de Média", xlab = "Tempo", ylab = "Número de Óbitos")
lines(previsoes$mean, col = "blue", lty = 2)
legend("topright", legend = "Previsões de Média", col = "blue", lty = 2)
plot(predict(previsoes))
df_previsoes <- data.frame(ds = seq(from = max(dados$ds), by = "months", length.out =
                                      numero_de_passos_a_prever),
                           previsao = previsoes$mean,
                           limite_inferior = previsoes$lower,
                           limite_superior = previsoes$upper)

ggplot() +
  geom_line(data = dados, aes(x = ds, y = numero_obitos), color = "black", size = 1) +
  geom_line(data = df_previsoes, aes(x = ds, y = previsao, linetype = "Previsões"), color =
              "blue") +
  geom_ribbon(data = df_previsoes, aes(x = ds, ymin = limite_inferior.80., ymax =
                                         limite_superior.80.), fill = "blue", alpha = 0.3) +
  labs(title = "Previsão de Óbitos com ARIMAX",
       x = "Tempo",
       y = "Número de Óbitos") +
  scale_linetype_manual(name = "Previsões", values = "dashed") +
  theme_minimal()
ts_dados_treino <- ts(dados_treino$numero_obitos, start = c(2012, 1), frequency = 12)

decomposicao <- decompose(ts_dados_treino)

par(mfrow = c(2, 2))
plot(decomposicao$trend, main = "Componente de Tendência", ylab = "Tendência")
plot(decomposicao$seasonal, main = "Componente Sazonal", ylab = "Sazonalidade")
plot(decomposicao$random, main = "Componente Residual", ylab = "Resíduo")
plot(ts_dados_treino, main = "Série Temporal Original", ylab = "Número de Óbitos")

summary(previsoes)

valores_obs <- dados_teste$numero_obitos
valores_prev <- previsoes$mean
r_squared <- 1 - sum((valores_obs - valores_prev)^2) / sum((valores_obs - mean(valores_obs))^2)
cat("R^2 do modelo:", r_squared, "\n")

accuracy_results <- accuracy(object = previsoes, x = dados_teste$numero_obitos)
r_squared_manual <- 1 - sum((dados_teste$numero_obitos - previsoes$mean)^2) /
  sum((dados_teste$numero_obitos - mean(dados_teste$numero_obitos))^2)


resultados_tabela <- data.frame(
  Modelo = "ARIMAX",
  Acuracia = accuracy_results[1],
  R2 = r_squared_manual
)
print(resultados_tabela)

desvio_padrao <- sd(previsoes$mean)
media <- mean(previsoes$mean)
coef_variacao <- (desvio_padrao / media) * 100
cat("Coeficiente de Variação do Modelo ARIMAX:", coef_variacao, "%\n")

residuos <- residuals(modelo_arimax)
shapiro.test(residuos)

acf_residuos <- acf(residuos, lag.max = 20, main = "Autocorrelação dos Resíduos")
plot(acf_residuos)

``````
