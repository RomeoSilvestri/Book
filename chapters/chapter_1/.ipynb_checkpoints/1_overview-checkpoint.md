---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Problem Definition

Problem Definition is the crucial initial phase in the data science lifecycle. During this phase, the primary objective is to clearly and comprehensively identify and articulate the problem that data analysis aims to address. This involves the following key aspects:

**1) Problem Identification**

In the initial phase, the critical first step is to meticulously pinpoint and articulate the problem that necessitates resolution through data analysis. This entails crafting a precise and unambiguous description of the problem, leaving no room for interpretation or ambiguity. The clarity of this problem statement serves as the foundation upon which the entire data science project is built. Ambiguities or inaccuracies at this stage can lead to misguided efforts and suboptimal outcomes in subsequent phases.

*The problem is to develop a predictive model that can accurately estimate the prices of residential properties in different neighborhoods of Madrid, facilitating better decision-making for both buyers and sellers.*


**2) Project Objective Determination**

Following the identification of the problem, the subsequent critical step is to establish well-defined project objectives. These objectives must adhere to the SMART criteria, ensuring that they are Specific, Measurable, Achievable, Relevant, and Time-bound. This approach ensures that the objectives are quantifiable, realistic, and closely aligned with the overarching business goals or specific contextual requirements. Well-defined objectives provide a clear sense of direction and serve as benchmarks for evaluating the project's success. Ensure that the project's objectives are attainable within the defined timeframe and allocated resources. The project timeline for model development, training, and evaluation will be designed to strike a balance between thorough analysis and efficient resource utilization.

*The primary objective is to minimize prediction error in estimating real estate prices across various neighborhoods in Madrid. The goal is to achieve a substantial reduction in prediction error when compared to baseline models, ultimately improving the accuracy of price predictions. Systematically compare the performance of spatial and non-spatial predictive models to identify the most accurate and effective approach for price prediction. Assess the accuracy of predictions at the neighborhood level within Madrid. The objective is to ensure that predictions are within a narrow margin of ±5% of the actual property prices for each neighborhood. This level of granularity will enable precise insights into property values within specific areas of the city.*

**3) Specification of Project Evaluation Metrics**

Central to the problem definition phase is the specification of project evaluation metrics. These metrics serve as the yardsticks for gauging the project's effectiveness and alignment with its objectives. They must be intricately tied to the project's goals and capable of quantifying the performance of proposed solutions. In the case of a problem involving the classification of fraudulent financial transactions, evaluation metrics might encompass accuracy, precision, recall, and the F1-score of the model. These metrics are carefully selected to provide a comprehensive view of the model's performance.

*To measure the success of the project and ensure alignment with the objectives, specific evaluation metrics are defined, including Mean Squared Error (MSE) and Mean Absolute Error (MAE): MSE quantifies the average squared difference between predicted and actual prices. The goal is to achieve an MSE of less than a specific value, for example 200.000 euros, indicating low overall prediction error, instead MAE measures the average absolute difference between predicted and actual prices. The target is to have an MAE of less than a specific value, demonstrating the model's ability to make accurate predictions.*

The Problem Definition phase necessitates active engagement with key stakeholders, including the data science team, business decision-makers, and domain experts. This collaborative effort ensures a holistic understanding of the problem's nuances, business context, and the desired outcomes. Furthermore, it is imperative to meticulously document this phase, creating a robust foundation to guide subsequent stages of the data science project and facilitating the validation of results upon project completion.

Properly defined problems act as a North Star throughout the project's lifecycle, steering it away from the pitfalls of "project drift," wherein the project veers off course from its initial objectives. A well-crafted problem definition is indispensable for the overall success and efficacy of the data science endeavor, aligning efforts with business needs and delivering actionable insights.