# Honeydew - Snowflake World Tour 2025 Hands-On Lab

## Introduction

In this session we will:
1. Bootstrap a semantic layer in Honeydew using some pre-created Semantic Views in Snowflake.
2. Iteratively enhance the semantic layer with additional definitions and metadata.
3. Ask complex analytical questions and get insights from the data, by leveraging an agentic flow using LLMs running in Cortex.
4. See how the same semantic layer can be used in BI tools.

## Setup

1. Signup to the Honeydew demo environment at https://demo.honeydew.cloud/signup
   You will automatically be added to the hands-on lab org, and will be able to explore the environment.
   
2. All the semantic layer metadata created during the lab is stored in this repository.
   You can browse the branches and detect the branch created by your user.

3. During the lab, you will be using a Honeydew-owned Snowflake account.
   If you would like to try Honeydew with your own data and semantics,
   you can sign up to a trial account at https://app.honeydew.cloud/signup.

## About the data

1. We are analyzing a schema of Airbnb listings and reviews.
2. The full data is available until the end of June 2025.
3. DISCLAIMER:
   The data used in this lab was taken from [Inside Airbnb](https://insideairbnb.com/) website, and is used under the    [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).


## Semantic modeling flow

### Creating a new branch

1. Create a new branch, give it a unique name.
   In Honeydew, users operate on branches when making changes to the semantic layer, and then can merge them to the `prod` version.

### Import Semantic View

1. Use `Import` and choose **Semantic View** option.
1. Choose the `HONEYDEW_SWT_DEMO.HONEYDEW_SWT_DEMO` schema.
1. Add the semantic view `AIRBNB` and click `Import`.

### Review data
1. What entities exist in the data? How are they connected to each other?
   Hint: use the graph visualization for the entities and the relationships.
3. What fields exist?
4. What is the time range of the fields?
5. What values do certain fields have? How can we slice and dice the data?

You can use the **Playground** section to explore the data.

<img width="181" height="254" alt="image" src="https://github.com/user-attachments/assets/e25155b3-c59f-4435-bcde-6d9848449683" />


### Create additional semantic definitions

Note: either follow the following instructions or create these in **Playground**, and then using the **Add to Entity** option.

1. Go to the `detailed_reviews` entity, add an **Attribute** named `review_month`, of type `date`
   with the definition `DATE_TRUNC(MONTH, detailed_reviews.date)`, and add it.

   Explanation: we want to use this attribute to group metrics by month.
   
1. Go to the `detailed_reviews` entity, add an **Metric** named `reviews_by_month`, of type `number`
   with the definition `detailed_reviews.count GROUP BY (*, detailed_reviews.review_month)`, and add it.

   Explanation: we want to use this metric to calculate number of reviews per month.
   
1. Go to the `detailed_reviews` entity, add an **Metric** named `avg_reviews_by_month`, of type `float`
   with the definition `AVG(detailed_reviews.reviews_by_month)`.
   Set the description to `Use this metric whenever asked about average reviews per month`, and add the metric.

   Explanation: this is a complex composite metric that can aggregate on top of the previous metric.
     
1. Go to the `Domains` section, edit the `airbnb` domain (using the `Edit` button on the right)
   and add the newly created `review_month`, `reviews_by_month` and `avg_reviews_by_month` fields to it.

   Explanation: We are curating the context of what the AI Analyst can use from the schema.
   It will only use items included in the domain.

1. Explore the description of the domain. It can be used to provide additional guidelines to the ai.
   You can later on experiment by changing it and seeing how that affects the AI answers.
   
## Deep Analysis

1. Navigate to the **Analyst** section.
1. **Important**: Use the selector on top, to choose the Airbnb domain, before you start to ask questions.
1. In the questions box, type in your question. You can ask follow-up questions as part of the conversation.

### Questions flow (recommended)

1. What is the average monthly number of reviews during the last 7 years?
2. Was there any anomaly? Can you explain it?
3. Can you focus on 2020-2022 and break it down by cities?
4. Can you explain why certain cities were impacted more than others?
5. Were there any specific segments of listings that were impacted more than others?


### Additional Sample questions

1. Do superhosts get higher rating? Does it change per city?
2. Are superhosts more successful, and why?
3. Which cities are more popular for familites
4. Which cities are affected and unaffected by seasonality
 

## Resources

During the session you can use the [Honeydew Documentation](https://honeydew.ai/docs/introduction)
