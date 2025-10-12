# Honeydew - Snowflake World Tour 2025 Hands-On Lab

## Introduction

In this session we will:
1. Bootstrap a semantic layer in Honeydew using some pre-created Semantic Views in Snowflake.
2. Iteratively enhance the semantic layer with additional definitions and metadata.
3. Ask complex analytical questions and get insights from the data.
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

1. We are analyzing a schema of Airbnb listings and reviews. The full data is available until end of June 2025.

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

You can start by creating these in **Playground**, and then using the **Add to Entity** option.

1. Add a `review_month` attribute of type `date` to the `detailed_reviews` entity, with the definition `DATE_TRUNC(MONTH, detailed_reviews.date)`.
1. Add a `reviews_by_month` metric, of type `number` to the `detailed_reviews` entity, with the definition `detailed_reviews.count GROUP BY (*, detailed_reviews.month)`.
1. Add an `avg_reviews_by_month` metric of type `number` to the `detailed_reviews` entity, with the definition `AVG(detailed_reviews.reviews_by_month`.
1. Go to the `avg_reviews_by_month` metric's `Advanced` tab, and add the following to the `AI Description`: `Use this metric whenever asked about average reviews per month`
1. Go to the `airbnb` domain and add the newly created `review_month`, `reviews_by_month` and `avg_reviews_by_month` fields to it.

## Analysis

1. What is the monthly number of reviews in the last 7 years?
2. Was there any anomaly? Can you explain it?
3. Can you focus on 2020-2022 and break it down by cities?
4. Can you explain why certain cities were impacted more than others?
5. Were there any specific segments of listings that were impacted more than others?


## Additional Sample questions

1. Do superhosts get higher rating? Does it change per city?
2. Are superhosts more successful, and why?
3. Which cities are more popular for familites
4. Which cities are affected and unaffected by seasonality
 

## Resources

During the session you can use the [Honeydew Documentation](https://honeydew.ai/docs/introduction)


## DISCLAIMER:
The data used in this lab was taken from [Inside Airbnb](https://insideairbnb.com/) website, under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
