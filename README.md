## Hospital Mortality Analysis and Forecast Report
This report provides a comprehensive analysis of the outcomes obtained through different prediction models applied to hospital mortality data, with a special focus on the COVID-19 pandemic. The examined models include ARIMAX, Bagging, and Boosting. Here are the key findings and conclusions:

### Key Findings:
Impact of the COVID-19 Pandemic: An analysis of the data revealed a significant increase in hospital mortality between 2020 and 2022, correlated with the COVID-19 pandemic. Long-term health complications in survivors and the spread of misinformation were identified as contributing factors to the persistence of the increasing mortality trend.

### Influencing Factors:
Age, economic conditions, and hospital costs associated with COVID-19 were identified as significant factors affecting mortality patterns.

### Risk Management and Hospital Governance:
Risk management strategies and hospital governance were highlighted as essential measures to address the challenges presented by the pandemic. Risk analysis and the promotion of a patient safety culture were emphasized as critical focus areas.

### Post-2022 Forecasts:
Post-2022 mortality forecasts indicate a growing trend, with estimated confidence intervals. Comparison with actual 2023 data shows overall consistency of forecasts with observed reality.

### ARIMAX Model:
The ARIMAX model adequately captured the temporal structure of the data. Significant coefficients were identified, highlighting the influence of different factors on hospital mortality. ARIMAX model forecasts suggest a growing trend in mortality post-2022, with reasonable consistency with actual 2023 data.

| Month / Year	 |	ARIMAX Forecast	 |	2023 Actual Data |
| --------- | ----------------| ----------------- |
| Jan / 2023	| 11.836	|11.144 |
| Feb/ 2023	| 11.358	| 9.883 |
| Mar/2023	| 12.740 |	11.345 |
| Apr/2023	| 13.626 |	10.871 |
| May/2023	| 13.615 |	11.338 |
| Jun/2023	| 13.864	| 12.373 |
| Jul/2023 |	13.876	| 12.399 |
| Ago/2023	| 12.920 |	12.286 |
| Sep/2023	| 12.055	| 11.565 |
| Oct/2023	| 11.720 |	10.998 |
| Nov/2023 |	11.496 | 11.163 |
| Dez/2023	| 11.142 |Not yet informed by the Ministry of Health. |

In Figure 1, we can infer that over the ten years, the months of January, June, July, and November experienced greater variability.


![image](https://github.com/nataliloure/MODELO-ARIMAX-VS-ENSEMBLE-DADOSHOSP/assets/138037869/f68a1d16-2784-4371-a698-a013ed60c0d5)

                                                     Figure 1. Boxplot graph of hospital deaths.


### Bagging Model with Random Forest (RF):
In addition to the ARIMAX model, a Bagging model with RF was applied to improve forecasts. Although it showed improvements in error rates after variable transformation, there is still room for enhancements in algorithm construction.

        
| Month / Year	 | 	Bagging Forecast	 | 2023 Actual Data |
| -------- | --------------------- | ------------------- |
| Dec / 2022	|11.726	| 11.024 |
| Jan / 2023	|12.375	| 11.144 |
| Mar / 2023	|11.774	| 11.345 |
| May / 2023	|12.093	| 11.338 |
| Jul / 2023	|11.808	| 12.399 |
| Ago / 2023	| 11.787	| 12.286 |
| Oct / 2023	|11.785	| 10.998 |
| Dec / 2023 |11.761	|Not yet informed by the Ministry of Health. |


### Boosting Model:
The Boosting model, using the XGBoost method, showed promise, with a growing trend in the number of deaths. Despite some flaws in month linearity, the XGBoost model exhibited relatively low error metrics compared to other models, suggesting superior performance.

| Month / Year	 |	XGBoost Forecast		| 2023 Actual Data |
| -------- | ----------------- |   --------------------    |
|Dec / 2022	|13.646  |     11.024            |
|Jan / 2023	|12.857	 |     11.144            |
|Mar / 2023	|10.789	|   11.345 |
|May / 2023	|11.247	|11.338 |
|Jul / 2023	|11.563	|12.399 |
|Ago / 2023	|11.511	|12.286 |
|Oct / 2023	|11.208	|10.998| 
|Dec / 2023	|11.004	|Not yet informed by the Ministry of Health. .|



### Conclusions:

#### Model Evaluation:
Comparative analysis of the models revealed that the Boosting model, especially using XGBoost, showed superior performance in terms of error metrics. The ARIMAX model also demonstrated solid results, offering valuable insights into explanatory variables.

#### Model Weighting:
Model weighting indicated that XGBoost has the highest final weight, suggesting a significant contribution to forecast accuracy. However, the ARIMAX model also contributed substantially, highlighting the importance of considering different approaches in predictive analysis.

#### Recommendations:
Risk Management and Hospital Governance:
The implementation of risk management strategies, based on insights provided by prediction models, is essential for effectively addressing the challenges posed by the pandemic and other public health issues.

#### Model Enhancement:
Continuous investments in research and development are recommended to improve the accuracy and robustness of prediction models, especially in public health contexts.

#### Integrated Approaches:
An integrated approach, combining insights from ARIMAX, Bagging, and Boosting models, can provide a more comprehensive and accurate view of hospital mortality trends, facilitating better decision-making.

#### Final Considerations:
The impact of the COVID-19 pandemic on hospital mortality is significant and complex. The findings of this study highlight the importance of advanced predictive approaches and adaptive risk management strategies to address ongoing challenges in the healthcare sector. The XGBoost model stands out as a promising tool for accurate predictions, while the ARIMAX model continues to offer valuable insights into factors underlying hospital mortality. These findings can guide policies and practices to improve the effectiveness of healthcare services and mitigate the adverse impacts of the pandemic.
