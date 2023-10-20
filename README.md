# DishSage

Team Members 
Karen Wang
sw3709@columbia.edu
Rohan Rabbi
mr4280@columbia.edu
Yi Quan (Bonny)
yq2311@barnard.edu
Ruoyu Chen
rc3506@columbia.edu


Problem statement: 
Whether we are ordering food in person or picking restaurants online, menus are one of the most important points of information. However, most menus are designed for general purposes without specific information for people with special dietary needs or preferences. This often results in extra effort to look up dishes online, ask waiters, or spend longer time reading through the entire menu. 

“What does a specific menu mean to you?” Our application will give you the answer. We want to build a tool that processes food menus, synthesizes information and provides a summary matching the overall collection of dishes to the users’ personal needs, including allergy history, nutrition needs, diet restrictions, religion, diet preferences, etc. A typical report after processing the menu may look like this:

Restaurant: David Burke Tavern
Most dominant food category: seafood (80%)
Recommended: cauliflower steak, roasted rack of lamb, wild mushroom ravioli
Avoid: fire roasted halibut, diver scallops, lobster salad
Your match: 20%
Reasoning: based on your profile, you should avoid food with high uric acid. Since most dishes in David Burke Tavern are seafood, we do not recommend dining here. 


Motivation:
This tool will customize the menu search experience for users, allowing them to “interpret” menus for themselves and quickly filter restaurants based on personal preferences. Meanwhile, it will save time and be a safeguard for people with special dietary restrictions.

Existing solutions/Literature Review:
We have not found an existing solution for this need. We believe that interpreting menus and generating insights based on user profiles is innovative. Additionally, we accept both text (through menu API) and image (using OCR techniques such as AWS Textract) menus, which is a very unique approach. 


Success criteria:
A frontend hosted on S3 and API Gateway handling requests (e.g. user uploads an image) and returns endpoints.
A user login system from the frontend and Amazon Cognito (ensures user uniqueness) for authentication. User profiles and static data are fetched from Amazon RDS.
A restaurant search function that will return the menu of the searched restaurant. Searchable data can be indexed in OpenSearch.
If a menu is an image, use AWS Textract to extract text, managed by a Lambda function; text data might be processed using AWS Comprehend for any specific NLP requirements.
Lambda functions interact with the OpenAI API (managed secrets manager) to generate reports detailing how well the menu matches with the user’s preference and need. This would also return a list of recommended dishes and do-not-eat dishes, as well as some summarization text.
Restaurant recommendation based on matching menus: use Lambda function to fetch restaurant/menu data from APIs (mentioned below in Data section) and store them in DynamoDB. Compare the menu data to user data, and add an endpoint in API Gateway for recommended restaurants.

Potential goals if time permits:
Group dining option: allowing users to invite friends into a dining group, and the system will access menus based on the group’s overall preference. 
Advanced OpenAI integration: We hope to use openai to provide more information about dishes (e.g. understanding Pad Thai often contains nuts even if not explicitly listed on menu), disease (e.g. gout patients should avoid food with high uric acid); Or have a database that matches potential ingredients to dishes. So it can catch ingredients that are not explicitly listed on the menu.
Users can also bookmark favorite menus, and reverse-search for restaurants that provide a specific dish.


Target audience:
People with special dietary restrictions due to health condition or religion, 
People with personal preferences or nutrition goals 
People who don’t want to spend time reading long menus when ordering food
People who want help picking restaurants that provides the dishes they like

Data:
Menu data: Toast has a menu API for all their restaurants: https://doc.toasttab.com/openapi/menus/operation/menusGet/
There are also many other menu APIs on Rapid API: https://rapidapi.com/search/restaurant%2Bmenu
Personal dietary preferences, which will be entered by users 
