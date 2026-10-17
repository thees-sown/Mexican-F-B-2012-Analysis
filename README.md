# Mexican-FnB-2012-Analysis
<img width="736" height="520" alt="image" src="https://github.com/user-attachments/assets/3aa8acf0-42f7-44a3-81aa-6f9e84102c39" />

Author: Phan Trần Thế Sơn

Date: June 2026

Tools Used: Power Query, Power BI

## 📋 Table of Contents:

1 - Background & Overview

2 - Dataset Description & Data Structure

3 - Design Thinking Process

4 - Key Insights & Visualizations

5 - Recommendation

## 📌 1 - Background & Overview

**🔎 What is this project about?**

This project aims to build a **Power BI dashboard** using the *Mexican Restaurants 2012* dataset, which includes data on Ratings, Consumers, Restaurant, Consumer Preferences and Restaurant Cuisines. The goal is to provide senior managers with **data-driven insights** to:

- Understand current performance of the Mexican F&B Industry in 2012
- Uncover consumer sentiment trends and evaluate how individual diner preferences drive rating behaviors
- Profile key attributes distinguishing high-performing, top-rated restaurants
- Deliver actional F&B domain insights to de-risk and optimize capital investment decisions

**👥 Who is this project for?**

✔️ **Data analysts and business analysts** exploring real-world applications of consumer sentiment analysis, feature profiling, and hospitality market intelligence

✔️ **Restaurant Owners & General Managers** seeking actionable benchmarks on service quality, pricing tiers, and dining attributes to elevate customer ratings.

✔️ **F&B Investors & Entrepreneurs** looking to de-risk capital allocation and identify high-potential restaurant concepts or locations.

**❓ What are the business questions?**

✔️ **Consumer Rating & Sentiment Dynamics:** What patterns define customer ratings across overall, food, and service dimensions, and where do the biggest rating disparities occur?

✔️ **High-Performing Restaurant Profiling:** What specific operational attributes (e.g., price range, cuisine type, alcohol service, smoking policy, parking) distinguish top-rated venues from underperforming ones

**✔️ Consumer Preference Alignment:** How strongly do individual diner traits (e.g., budget levels, preferred cuisine, lifestyle habits, transportation) correlate with their actual ratings and dining choices?

**✔️ Strategic Investment & Market Feasibility:** Which cuisine types, price tiers, and dining concepts present the highest market demand and customer satisfaction for potential F&B investment?

**🎯 What are the outcomes of the project?**

✔️ Food quality achieved satisfactory baseline scores (1.22/2.0), whereas service consistency lagged substantially behind (1.09/2.0).

✔️ Young demographics, including Young Adults and Young Workers, drove peak patronage and review volume, yet registered the lowest net satisfaction across all age brackets.

✔️ Overall Scores aligned closely with culinary quality (1.21 vs. 1.18), but service execution consistently lagged behind across all operational metrics.

✔️ Despite the fact that the majority of customers had Medium budget, many customers were willing to pay extra for curated experiences.

## 📂 2 - Dataset Description & Data Structure

**📌 Data Source:**

- Source: Kaggle
- Size: The Ratings table contains 1,161 records

**📊 Data Structure & Relationships:**

1️⃣ The dataset consists of four tables:

- **Ratings** (Fact Table - 1,161 records): Captures transactional rating interactions evaluated across three core performance dimensions (Overall, Food, and Service) by individual consumers per restaurant
<details>
<summary> <strong>Table 1: Ratings</strong></summary>

| Column Name       | Data Type   | Description                              |
|------------------|------------|------------------------------------------|
| `Consumer_ID`      | `VARCHAR`   | Unique identifier for each customer.       |
| `Restaurant_ID`    | `DATE`      | Unique identifier for each restaurant.         |
| `Overall_Rating`     | `INT`      | Overall Score (/2) given to each restaurant by each customer.        |
| `Fodd_Rating`     | `INT`      | Food Score (/2) given to each restaurant by each customer.        |
| `Service_Rating`     | `INT`      | Service Score (/2) given to each restaurant by each customer.        |

</details>

- **Customers** (Dimension Table - 138 records): Stores granular demographic, socio-economic, and behavioral profile attributes of surveyed consumers.
<details>
<summary><strong>Table 2: Customers</strong></summary>
| Column Name             | Data Type | Description                                                                 |
|-------------------------|-----------|-----------------------------------------------------------------------------|
| `consumer_id`           | `VARCHAR` | Unique identifier for each diner.                                           |
| `city`                  | `VARCHAR` | The diner's city of residence.                                              |
| `state`                 | `VARCHAR` | The diner's state of residence. |
| `country`               | `VARCHAR` | The country of residence (Standardized to 'Mexico').                        |
| `latitude`              | `FLOAT`   | Geolocation coordinate for spatial mapping.                                 |
| `longitude`             | `FLOAT`   | Geolocation coordinate for spatial mapping.                                 |
| `smoker`                | `VARCHAR` | Smoking habit. |
| `drink_level`           | `VARCHAR` | Alcohol consumption frequency.       |
| `transportation_method` | `VARCHAR` | Primary commute type.  |
| `marital_status`        | `VARCHAR` | Relationship status.    |
| `children`              | `VARCHAR` | Presence of dependents.    |
| `age`                   | `INTEGER` | The diner's age.        |
| `occupation`            | `VARCHAR` | Employment status.   |
| `budget`                | `VARCHAR` | Self-reported spending tier. |

</details>

- **Restaurants** (Dimension Table - 130 records): Profiles operational venue characteristics, including pricing tiers, infrastructure/amenities, licensing, and environmental policies.
<details>
<summary><strong>Table 3: Restaurants</strong></summary>
| Column Name       | Data Type | Description                                   |
|-------------------|-----------|-----------------------------------------------|
| `restaurant_id`   | `VARCHAR` | Unique identifier for each restaurant.        |
| `restaurant_name` | `VARCHAR` | The name of the dining venue.                 |
| `city`            | `VARCHAR` | The city where the restaurant is located.     |
| `state`           | `VARCHAR` | The state where it operates.                  |
| `country`         | `VARCHAR` | The country of operation.                     |
| `zip_code`        | `VARCHAR` | The local postal code.                        |
| `latitude`        | `FLOAT`   | Geolocation coordinate for spatial mapping.   |
| `longitude`       | `FLOAT`   | Geolocation coordinate for spatial mapping.   |
| `alcohol_service` | `VARCHAR` | Type of alcohol service provided.             |
| `smoking_allowed` | `VARCHAR` | The venue's smoking policy.                   |
| `price`           | `VARCHAR` | The pricing tier of the restaurant.           |
| `franchise`       | `VARCHAR` | Indicates if the venue is a chain or independent. |
| `area`            | `VARCHAR` | The seating environment type.                 |
| `parking`         | `VARCHAR` | Parking availability for customers.           |

</details>

- **Customer Preferences** (Dimension Table - 330 records): Maps multi-label culinary interests and cuisine preferences associated with each consumer
<details>
<summary><strong>Table 4: Customer Preferences</strong></summary>
| Column Name         | Data Type | Description                                   |
|---------------------|-----------|-----------------------------------------------|
| `consumer_id`       | `VARCHAR` | Unique identifier for each diner.             |
| `preferred_cuisine` | `VARCHAR` | The specific type of cuisine preferred.       |
</details>

- **Restaurant Cuisines** (Dimension Table - 112 records): Details the primary culinary classifications and cuisine specializations across restaurant profiles.
<details>
<summary><strong>Table 5: Restaurant Cuisines</strong></summary>

| Column Name     | Data Type | Description                                   |
|-----------------|-----------|-----------------------------------------------|
| `restaurant_id` | `VARCHAR` | Unique identifier for each restaurant.        |
| `cuisine`       | `VARCHAR` | The specific type of cuisine served.          |
  
</details>

#### Data relationships:
<img width="575" height="358" alt="image" src="https://github.com/user-attachments/assets/2fbb8039-d18e-4b07-99fc-2655d10bb36f" />

| **From Table** | **To Table** | **Join Key**   | **Relationship Type**                                  |
|------------|----------|------------|----------------------------------------------------|
| `fact_ratings` | `dim_customers` | `Consumer_ID` | Many-to-One (multiple ratings belong to one Customer) |
| `fact_ratings` | `dim_restaurants` | `Restaurant_ID` | Many-to-One (multiple ratings can be given to one Restaurant) |
| `dim_restaurants` | `dim_restaurant_cuisines` | `Restaurant_ID` | One-to-Many (one Restaurant can serve more than one Cuisine) |
| `dim_customers` | `dim_customer_preferences` | `Consumer_ID` | One-to-Many (one Customer can have more than one Cuisine Preference) |

## 🧠 3 - Design Thinking Process
### 1️⃣ Empathize
<img width="1920" height="1080" alt="3" src="https://github.com/user-attachments/assets/fd004f06-66d4-404e-b2d3-a51e0fcca1c1" />

<img width="1920" height="1080" alt="4" src="https://github.com/user-attachments/assets/9cf6b24e-bca3-4ab1-9a23-8b9dbeaa23f5" />

### 2️⃣ Define Point of View
<img width="1920" height="1080" alt="5" src="https://github.com/user-attachments/assets/29b87832-3049-4833-9722-0d1c5831bae5" />

### 3️⃣ Ideate
<img width="1920" height="1080" alt="6" src="https://github.com/user-attachments/assets/7ae060e5-fe4a-477b-810b-453e16e4d33f" />

<img width="1920" height="1080" alt="7" src="https://github.com/user-attachments/assets/7129b2a3-f043-48f7-9dac-3ecc63fe10b7" />

## 📊 4 - Key Insights & Visualizations
### I. Overview
<img width="1920" height="1080" alt="Overview" src="https://github.com/user-attachments/assets/1ec6e9ea-e8cd-4800-851d-d9535b9492ce" />

#### 📌 Key Findings:

1 - Systemic Service Deficit & Rating Distribution Skew

- **Food Quality Aligns with Consumer Taste:** Both **Overall** and **Food** ratings peaked at the maximum score (**2.0**), registering **486** and **516** top ratings respectively. This affirms that culinary offerings reliably meet diner expectations.
- **Service** ratings exhibited an inverse distribution:
    - The mode shifted down to a mediocre score of **1.0**.
    - It captured the highest concentration of minimum scores (**0.0**) across the dataset.
    
    → While culinary execution remains resilient, frontline service delivery constitutes a severe operational friction point and a major drag on overall customer retention.
    

2 - Geographic Distribution & Regional Performance

- **Current Landscape:** Most Mexican restaurants are centered in **San Luis Potosí (84 venues)**, while coverage remains quite limited in **Morelos (23)** and **Tamaulipas (23)**.
- Regional Satisfaction disparities:
    - Despite having the highest venue density, **San Luis Potosí** maintains a healthy **Overall Rating of 1.21/2.0** (ranking second).
    - **Morelos**, with only 23 restaurants, achieved the highest satisfaction score across all regions (**1.37/2.0**).
    - In contrast, while **Tamaulipas** shares the exact same venue count (23), its average rating lags significantly behind at just **0.93/2.0**.
    
    → Promising Markets are San Luis Potosi and Morelos: Both regions showcase strong market potential driven by highly receptive diners. Morelos stands out as a prime target for expansion thanks to high customer satisfaction paired with low market saturation, while San Luis Potosí offers a proven, stable demand base.
    
    → Caution required for Tamaulipas: the low rating (0.93) coupled with low venue density suggests that market hesitation may stem from deeper operational friction or weak diner enthusiasm rather than just a supply gap. Any expansion into Tamaulipas requires thorough localized market research before committing capital.
    

3 - Underperformance & Operational Risks in Tamaulipas

Top 10 Restaurants across core dimensions: Food, Overall and Service

- **Food Quality:** **Morelos** and **San Luis Potosí** dominated the leaderboard with **5** and **4** venues respectively, whereas **Tamaulipas** managed only a single entry (**1**).
- **Overall & Service Excellence:** The top 10 rankings across both dimensions were entirely split between San Luis Potosí and Morelos. **Tamaulipas had zero representation** on either list.

**→ Systemic Service & Quality Gap:** The complete absence of Tamaulipas from the top-tier Overall and Service rankings confirms that its low regional average (0.93) is not skewed by a few outliers, but reflects widespread operational challenges across local venues.

→ **Investment Caution:** Entering Tamaulipas at this stage carries notable risks. Without existing high-standard benchmarks to model after, new entrants would likely face steeper hurdles in staff training, supply consistency, and changing local diner perceptions. Capital allocation is much better prioritized for Morelos and San Luis Potosí.

### II. Customer Analysis
<img width="1920" height="1080" alt="Customers" src="https://github.com/user-attachments/assets/e24fe277-e128-49dd-aa9b-60320ed5ffb2" />

#### 📌 Key Findings:

1 - Core Demographic Profile of Satisfied Diners:

Customers reporting medium-to-high satisfaction share a distinct profile:

- **Age Cohort:** Young Adults and Young Workers
- **Marital Status:** Single
- **Budget Tier:** Medium
- **Primary Occupation:** Student
- **Children:** Independent (No children)
- **Smoking Habit:** Non-smoker
- **Alcohol Consumption:** Abstemious (Non-drinker / Occasional)
- **Commute Mode:** Public transit

2 - Regional Customer Volume vs. Satisfaction Rates

- **San Luis Potosí:** Attracted the largest diner base (**86 customers**), with a strong **73.4%** reporting medium-to-high satisfaction.
- **Morelos:** Despite a smaller customer footprint (**27 customers**), it achieved the highest proportion of satisfied diners at **75%**.
- **Tamaulipas:** Underperformed on both fronts - capturing only **25 customers**, with satisfaction dropping to **60%**.
    
    → **High Market Receptivity (San Luis Potosí & Morelos):** Both regions demonstrate healthy customer appetite. San Luis Potosí proves its ability to sustain high satisfaction across a large consumer volume, while Morelos shows strong baseline sentiment despite lower footfall, making both attractive targets for dining operations.
    
    **→ Diverging Challenge in Tamaulipas:** The combination of limited customer reach and lower satisfaction (60.0%) suggests that dining concepts in Tamaulipas face broader adoption barriers. Rather than expanding footprint here, efforts would need to address the root causes of diner dissatisfaction before attempting to scale customer volume.
    

3 - Culinary Preference Patterns in potential markets

- Top Cuisine Alignment: In the top-performing states of San Luis Potosí and Morelos, diner preferences within the top 10 cluster heavily around Mexican, Japanese, Coffee Shop, and Breakfast concepts.
    
    → **Core vs. Specialized Offerings:** Local Mexican food remains a reliable choice with steady demand, while Japanese cuisine shows that customers are also receptive to other popular options.
    
    → **Daytime Dining Opportunities:** The preference for coffee shops and breakfast suggests good potential for daytime visits, offering restaurants a practical way to attract customers outside of standard lunch and dinner hours.

### III. Restaurant Analysis
<img width="1920" height="1080" alt="Restaurants" src="https://github.com/user-attachments/assets/c6aa3da0-aed7-4f32-ac1b-87dfd0b515e9" />

1 - Consistency of the Food vs. Service Gap across Venue Features

- Across every restaurant characteristic examined, including Alcohol Service, Franchise status, Parking availability, Price tier, Smoking policy, and Area/Environment, Food scores consistently surpassed Service scores.
    
    → The gap between food quality and service delivery is not isolated to specific restaurant types or price levels. Rather, it appears across the entire dining landscape.
    
    **→ Clear Priority for Management:** Enhancing physical amenities or menu items will have limited impact on overall ratings if frontline service remains neglected. Operators across all categories would see better rating improvements by prioritizing staff training and smoother service workflows.
    

2 - Price Tier Performance & Customer Spending Behavior

- Rating Performance by Price: Restaurants in the Medium price range captured the highest review volume, the largest number of satisfied diners, and led across all three dimensions (Overall, Food, and Service). However, High-price restaurants demonstrated a comparable level of satisfaction and quality scores.
- Budget vs. Spending Alignment: Although earlier demographic data indicates that most diners identify with a Medium budget, a meaningful share of customers actively choose and positively rate High-price venues.
    
    → The success of higher-priced venues suggests that diners are willing to stretch their typical budgets for better food or an elevated dining atmosphere, pointing to healthy demand for premium concepts rather than strict price resistance.
    

3 - Regional Concentration of High-Quality Restaurants

- **San Luis Potosí:** Accounts for the bulk of restaurants (**84 venues**), with a very solid **81.76%** classified as high quality.
- **Morelos:** Despite a smaller market footprint (**23 venues**), it achieves an outstanding quality rate, with **94%** of its restaurants meeting high-quality benchmarks.
- **Tamaulipas:** Shares the same venue count as Morelos (**23 venues**), yet only slightly over half (**56%**) meet high-quality standards
    
    → Morelos sets an impressive quality standard that makes it an appealing, low-risk environment for quality dining concepts. San Luis Potosí successfully pairs high venue volume with dependable quality, confirming a well-developed local market.
    
    → The sharp drop in quality rate in Tamaulipas (56.0%) indicates widespread inconsistency in local operations. New entrants here would face a less established hospitality ecosystem, making expansion there notably more challenging.
    

4 - Profiling Top-Tier Excellence ("Restaurant Las Mañanitas")

- **Excellence Criteria:** Under the strict benchmark where an **"Excellent"** rating requires a perfect score (**2.0 across Overall, Food, and Service**), only a single venue qualified: **Restaurant Las Mañanitas** in **Morelos**.
    
    **→ Key Operational Attributes:**
    
    - **Beverage & Dining Environment:** Serves Wine & Beer, enforces a non-smoking policy, and provides an indoor (closed) dining setting.
    - **Business Model & Accessibility:** Operates independently (non-franchise), positions in the High price tier, and offers on-site customer parking.
- When comparing Las Mañanitas with near-perfect benchmark venues, core operational characteristics remained largely consistent, with slight variance appearing primarily in Alcohol Service policies and Parking Availability.

## 🔎 5 - Recommendation
| **Strategy**                     | **Insight**                                                                                                                                                       | **Recommendation**                                                                                                                                                                      |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **🍴 1. Frontline Service Overhaul** | - **Food** scores consistently outperformed **Service** scores across all restaurant categories and amenities. <br> <br> - **Service** remains the primary friction point lowering overall customer satisfaction.| Prioritize service quality improvements over aesthetic renovations or menu expansion by establishing standardized frontline training, refining floor workflows, and introducing real-time feedback checks to address service bottlenecks. |
| **🌍 2. Targeted Geographic Expansion** | - **San Luis Potosí** represents a large, stable market (**86 customers, 81.8% high-quality venues**). <br> <br> - **Morelos** shows high satisfaction and low saturation (**75% satisfaction, 94% high quality**). <br><br> - **Tamaulipas** lags across all metrics (**0.93 average rating, 0 venues in the top 10**) | - Direct new capital toward **Morelos** to capitalize on high customer receptivity with limited competition, while maintaining a steady presence in **San Luis Potosí**. <br> <br> - Treat **Tamaulipas** as high-risk, holding off on site openings pending further local research.|
| **👥 3. Persona-Aligned Operations** | - The **most satisfied diners** are single students and young professionals who commute via public transit, maintain non-smoking habits, and consume little to no alcohol. | - Select locations near public transit lines, campuses, or office hubs. Maintain smoke-free dining spaces, expand quality non-alcoholic and low-ABV beverage options, and offer practical promotions tailored to solo or young diners.|
| **📙 4. Daypart & Menu Diversification** | - Diners in top-performing regions (**San Luis Potosí, Morelos**) show strong interest in Japanese cuisine, Coffee Shops, and Breakfast alongside traditional Mexican food. | - Extend operational dayparts by introducing morning breakfast and afternoon coffee service to capture daytime foot traffic outside standard peak hours, while exploring selective menu items to add variety.|
| **🏠 5. Excellence Operational Blueprint** | - Perfect-rated venues (Restaurant Las Mañanitas) and near-perfect benchmarks consistently operate independently with enclosed indoor seating, non-smoking policies, high price positioning, and dedicated parking. | - For high-end concept development, adopt an independent operational model to maintain strict quality control, provide enclosed climate-controlled dining, ensure convenient parking, and deliver a consistently structured guest experience.|

