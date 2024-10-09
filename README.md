This project evaluates the responses of various chatbots using LLM as Judge to measure the factuality of the response and Cosine Similarity.The goal of this project was to evaluate how well four AI bots (Mia, Mike, Olivia, Bella) generated responses compared to expected target responses. For each question, we had:

* A target response (the correct or expected answer)
* A bot response (generated by each bot)
* A cosine similarity score (which measures the semantic closeness of the bot response to the target response)
The evaluation was conducted in two main steps:

## LLM as a Judge
LLM as a Judge is using LLMs to evaluate the responses of the bots, in comparison to the expected output. The responses are sent to an LLM with an evaluation prompt, and then ask the LLM to compare the response to the expected response, and score the response in three classes, Accurate, Partically Accurate, and Inaccurate. Responses were classified into three categories—ACCURATE, PARTIALLY ACCURATE, and INACCURATE—based on how closely the bot responses aligned with the target responses, and also an explantion on why the response belongs to that particular category.


### How it works:
* Text Conversion: Both the bot's responses and the expected responses are converted into numerical representations (vectors).The sentence_transformers library is used to convert text into numerical embeddings.

* Vector Calculation: These numerical representations are then converted into vectors in a high-dimensional space.The cosine of the angle between these two vectors is computed. A value closer to 1 indicates a higher similarity between the two signatures, while a value closer to 0 indicates lower similarity.

# Data Structure
The dataset we analyzed contains multiple columns for each bot, including:

* Question: The question posed to the bot.
* Target Response: The expected answer for each question (specific to each bot).
* Bot Response: The response generated by the bot.
* Cosine Similarity: The cosine similarity score between the target response and the bot response.
* Accuracy: The label assigned to each bot's response, indicating whether it was ACCURATE, PARTIALLY ACCURATE, or INACCURATE.
* Explanation: A brief description of why a particular accuracy label was assigned.

Each bot (Mia, Mike, Olivia, Bella) had its own set of responses, target responses, cosine similarity scores, and accuracy labels.

# Evaluating Semantic Similarity using Cosine similarity
Cosine similarity is a measurement that quantifies the similarity between two or more vectors. It is the cosine of the angle between vectors. A score closer to one, means the angle between two vectos is smal, which means they are more similar.
### How Cosine Similarity WOrks
Texts is converted into vectors. Each dimension of the vector represents a word from the document, with its value indicating the frequency or importance of the word. 
Cosine Similarity effectively captures the orientation or direction of the vectors and not their magnitude, making it reliable measure of similarity in texts of varying lengths.
### Results
The evaluation is based on cosine similarity between the bot's responses and the expected response. Cosine similarity is used in this context to measure the semantic similarity between the the bot responses and the expected response. 
| Bot    | Mean Cosine Similarity | Standard Deviation | Minimum | Maximum |
|--------|------------------------|--------------------|---------|---------|
| Olivia | 0.8978                 | 0.1135             | 0.3694  | 1.0000  |
| Mike   | 0.8367                 | 0.1595             | 0.1473  | 1.0000  |
| Bella  | 0.8361                 | 0.1734             | 0.1887  | 1.0000  |
| Mia    | 0.8269                 | 0.1881             | 0.1749  | 1.0000  |




Overall Similarity: All four bots have a relatively high mean cosine similarity score, indicating that their responses generally align well with the target response.
Variability: The standard deviation values vary among the bots, suggesting different levels of consistency in their responses. Olivia has the lowest standard deviation, indicating more consistent responses, while Bella and Mia have higher standard deviations, suggesting more variability.
Extremes: The minimum and maximum values for each bot reveal the range of similarities. All bots have at least one response that perfectly matches the target (cosine similarity of 1), but they also have responses that are less similar (cosine similarity below 0.5).

Contextual Factors: While a high cosine similarity suggests a good match, it's essential to consider the overall context of the conversation. A bot might generate a response that is semantically similar but misses the intended meaning due to lack of context.





# Accuracy Evaluation
Evaluated the accuracy of each bot's responses using the following three categories:

ACCURATE: The bot response was completely factually correct and aligned with the target response.
PARTIALLY ACCURATE: The bot response was somewhat correct but contained either partial misinformation or lacked full details.
INACCURATE: The bot response was factually incorrect or contradicted the target response.

## Accuracy Distribution
The distribution of accuracy levels for each bot was as follows:
![Mia](Images/Mia_distribution_plot.png) . 

Mia's Percentage of Responses by Accuracy Level was as follows:![Mia_Accuracy_Percentage](Images/Mia_Percentage_Accuracy.png) 

Mia has a strong performance with 73 accurate responses which is 86.9%, showing that most of her answers closely align with the target responses.
Only 5 responses are marked as inaccurate which is 6%, meaning Mia generally provides semantically correct answers, with minimal mistakes.
Few Partially Accurate Responses: There are 6 cases where Mia's responses are somewhat correct but contain either minor inaccuracies or incomplete information.
Mia is performing well overall, with the majority of responses (close to 90%) being accurate or partially accurate. The bot seems to struggle minimally with inaccurate answers.
 ![Bella](Images/Bella_Distribution_plot.png)
 
  Bella's Percentage of Responses by Accuracy Level was as follows:![Bella_Accuracy_Percentage](Images/Bella_percentage_Accuracy.png) 

 Bella performs similarly to Mia and Olivia, with 64 responses being accurate(76.2%), which suggests strong alignment with the target answers.
Bella has 13 partially accurate responses (15.5%), which is higher than Mia and Olivia, indicating that Bella sometimes provides answers that are somewhat correct but may miss some details.
Bella has only 7 inaccurate responses (8.3%), a relatively small number compared to Mike, showing that Bella makes fewer errors overall.
Conclusion:
Bella exhibits high accuracy, with (76.2%)her responses being accurate or partially accurate. The low number of inaccurate responses indicates that Bella generally provides reliable answers.

![Olivia](Images/Olivia_Distribution_plot.png) 

Olivia's Percentage of Responses by Accuracy Level was as follows:![Olivia_Accuracy_Percentage](Images/Olivia_Percentage_Accuracy.png)

Olivia demonstrates solid performance, with 65 responses classified as accurate, indicating high alignment with the target answers.
Olivia's 12 inaccurate responses suggest occasional errors, but they are relatively infrequent.
Similar to Mia, Olivia has a small number of responses (7) that fall between accurate and inaccurate, indicating that her understanding is generally strong but sometimes incomplete.
Olivia shows a high level of accuracy, with 77.4% of her responses being accurate. However, the presence of 12 inaccurate responses points to areas where the model could be improved.

![Mike](Images/Mike_Distribution_plot.png) 

Mike's Percentage of Responses by Accuracy Level was as follows:

![Mike_Accuracy_Percentage](Images/Mike_Percentage_Accuracy.png)

Mike's responses are more evenly distributed across the accuracy categories compared to Mia. While 34 answers are accurate which accounts to 40.5%, nearly as many (27) are only partially accurate whci is 32.1%, and 23 responses are fully inaccurate which is 27.4%.
With 23 inaccurate responses, Mike demonstrates a much higher tendency to generate incorrect answers compared to Mia, suggesting either misunderstandings or significant deviations from the target answers.
Mike seems to often generate responses that are somewhat correct but lack full alignment with the target answers due to the Large Proportion of Partially Accurate Responses which is 32.1%
Mike's performance is mixed, with nearly 50% of his responses being inaccurate or partially accurate.