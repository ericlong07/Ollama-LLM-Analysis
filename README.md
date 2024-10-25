# Background
[Ollama](https://github.com/ollama/ollama) is a tool that simplifies running open-source LLMs locally. It provides an easy way
to download, run, and experiment with various models from Hugging Face and other sources. 

All models in the following sections were run on a 2020 MacBook Pro with 2 Intel Core i5 processors.

# 1) Models Overview
| Model         | Parameters | Size  | Download              | Company     |
|---------------|------------|-------|-----------------------|-------------|
| Llama 3.2     | 3B         | 2.0GB | `ollama run llama3.2`  | Meta        |
| Mistral       | 7B         | 4.1GB | `ollama run mistral`   | Mistral AI  |
| Phi 3 Medium  | 14B        | 7.9GB | `ollama run phi3:medium` | Microsoft  |

For this comparison, I selected three LLMs from different organizations: **Llama 3.2** by Meta, **Mistral** by Mistral AI, and **Phi 3 Medium** by Microsoft. These models represent a range of parameter sizes (3B, 7B, and 14B, respectively), offering a balanced evaluation across small, medium, and large models. 

I chose **Llama 3.2** because it is a lightweight model (3B parameters), known for efficient performance in general language tasks while maintaining a small memory footprint (2.0GB), making it ideal for quick inference. **Mistral** is a 7B parameter model, which provides a middle ground between efficiency and performance, and is designed for versatility. Lastly, I included **Phi 3 Medium** due to its larger size (14B parameters), offering higher complexity and depth in generating responses, which is essential for understanding the performance of larger-scale models in comparison to smaller ones.

These three models, with their varying sizes, allow for a comprehensive comparison in terms of speed, accuracy, and resource requirements, providing insights into how model scale impacts general question answering tasks.

# 2) Basic Model Exploration

## a) General Question Answering
**Prompt**: How many r's in strawberry?

### Llama 3.2 Output
<img width="613" alt="image" src="https://github.com/user-attachments/assets/e94d6657-dc93-4057-b7c4-a6b8132e548e">

### Mistral Output
<img width="613" alt="image" src="https://github.com/user-attachments/assets/17ed3448-4e6f-4196-9d40-343b39bbf318">

### Phi 3 Medium Output
<img width="613" alt="image" src="https://github.com/user-attachments/assets/abfbcc26-5e54-4337-ad2d-0416ffbc754e">

### Summary
| Model         | Response                                       | Quality   | Speed    | Resource Usage |
|---------------|------------------------------------------------|-----------|----------|----------------|
| Llama 3.2     | There are 2 R’s in the word “strawberry”.       | Incorrect | 1.171s   | 3% CPU         |
| Mistral       | There are three ‘r’s in the word ”strawberry.”  | Correct   | 12.809s  | 0% CPU         |
| Phi 3 Medium  | There are two ‘r’ letters in the word “strawberry”. | Incorrect | 24.372s  | 0% CPU         |

- **Response Quality**: 
  - **Mistral** was the only model that produced the correct answer, identifying that there are three 'r's in "strawberry." 
  - Both **Llama 3.2** and **Phi 3 Medium** incorrectly stated that there are two 'r's.
  
- **Speed**:
  - **Llama 3.2** was by far the fastest, generating a response in just **1.171 seconds**.
  - **Mistral** took significantly longer at **12.809 seconds**, while **Phi 3 Medium** was the slowest, with a response time of **24.372 seconds**.
  
- **Resource Usage**:
  - **Llama 3.2** used **3% CPU** during its execution, while both **Mistral** and **Phi 3 Medium** registered **0% CPU** usage during their runs. This suggests that despite its fast speed, Llama 3.2 may have a slightly higher impact on system resources compared to the other two models.

Overall, **Mistral** delivered the correct answer but at a higher latency, while **Llama 3.2** provided the fastest response but was inaccurate. **Phi 3 Medium** had the slowest response and also delivered an incorrect answer.

## b) Text Summarization
**Prompt**: Summarize the following text: The Amazon rainforest, known as the "lungs of the Earth," is crucial for regulating the global climate and is home to a rich diversity of plants and animals. Covering over 5.5 million square kilometers, it absorbs significant amounts of carbon dioxide, helping combat climate change. However, deforestation from agriculture and logging threatens this ecosystem, leading to habitat loss and decreased biodiversity. Conservation efforts are vital to protect this essential resource.

### Llama 3.2 Output
<img width="749" alt="image" src="https://github.com/user-attachments/assets/fac30883-ceb7-4ff5-897d-2431262edf55">

### Mistral Output
<img width="910" alt="image" src="https://github.com/user-attachments/assets/aee84d4b-038a-4a67-a202-4ec463d03566">

### Phi 3 Medium Output
<img width="884" alt="image" src="https://github.com/user-attachments/assets/731c491f-0c55-4194-bbee-9968586efa99">

### Summary
| Model         | Response                                                                                                                                                                                                                                                                                                                                                  | Quality | Speed     | Resource Usage |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----------|----------------|
| Llama 3.2     | The Amazon rainforest is vital for regulating the global climate and supporting a vast array of plant and animal life. It absorbs significant amounts of carbon dioxide, but deforestation threatens its survival due to agriculture and logging.                                                                                                     | Decent  | 14.541s   | 0% CPU        |
| Mistral       | The Amazon Rainforest, often referred to as the “lungs of the Earth,” plays a significant role in regulating the global climate by absorbing carbon dioxide and aiding in combating climate change. Spanning over 5.5 million square kilometers, it houses a vast array of plant and animal species. However, the rainforest faces threats due to deforestation caused by agriculture and logging activities, leading to habitat loss and reduced biodiversity. The importance of conservation measures is emphasized to protect this vital resource. | Almost as long as the original text | 43.034s | 0% CPU        |
| Phi 3 Medium  | The Amazon rainforest is essential for global climate regulation and contains diverse flora and fauna over 5.5 million sq km; however, deforestation due to agriculture and logging endangers its biodiversity. Preservation efforts are necessary to safeguard this vital resource.                                                                                 | Effective | 1m2.79s  | 0% CPU        |

- **Response Quality**:
  - **Llama 3.2**: Provided a decent overview of the Amazon rainforest's importance, focusing on its role in climate regulation and the threat posed by deforestation. However, it lacks depth compared to the other models.
  - **Mistral**: Delivered a comprehensive response, emphasizing the rainforest's significance as the "lungs of the Earth" and detailing its vast area and biodiversity. It also highlights the importance of conservation measures, making it very informative.
  - **Phi 3 Medium**: Offered an effective summary that captures the essential points regarding climate regulation, biodiversity, and the need for preservation efforts. While concise, it successfully communicates the key information without being overly verbose.

- **Speed**:
  - **Llama 3.2**: Generated the response in 14.541 seconds, which is relatively quick compared to the other models.
  - **Mistral**: Took longer at 43.034 seconds, likely due to its more elaborate response that included detailed explanations and examples.
  - **Phi 3 Medium**: The slowest at 1 minute and 2.79 seconds, despite its concise response, indicating possible overhead in processing.

- **Resource Usage**:
  - All models demonstrated similar resource usage, with 0% CPU consumption during execution, suggesting efficient processing across the board.

In summary, while **Llama 3.2** provided a decent response quickly, **Mistral** offered a more detailed summary that was almost too similar to the original text. **Phi 3 Medium** was effective in its brevity but took the longest to generate a response. All models used minimal resources, indicating good efficiency. Depending on the context, **Mistral** may be preferable for re-wording, while **Llama 3.2** and **Phi 3 Medium** might be more suitable for actual summarization.

## c) Simple Code Generation
**Prompt**: Write a simple Python function that takes a list of numbers as input and returns the average of those numbers.

### Llama 3.2 Output
<img width="948" alt="image" src="https://github.com/user-attachments/assets/3d17e4d2-d479-435a-8448-3d07557a1463">

### Mistral Output
<img width="940" alt="image" src="https://github.com/user-attachments/assets/97de537f-da0e-4635-be44-9df24146a382">

### Phi 3 Medium Output
<img width="924" alt="image" src="https://github.com/user-attachments/assets/ea1b0879-e15f-4378-90d1-f35c781d2a55">

### Summary



## d) Creative Writing
**Prompt**: Write a one stanza poem about writing a poem.

### Llama 3.2 Output
<img width="612" alt="image" src="https://github.com/user-attachments/assets/51be09e7-69c4-4fec-a49f-d2f3f24b81f0">

### Mistral Output
<img width="612" alt="image" src="https://github.com/user-attachments/assets/c26ab3a2-ab6c-4dcb-9fb8-f7b6ed096b71">

### Phi 3 Medium Output
<img width="612" alt="image" src="https://github.com/user-attachments/assets/be477d79-7704-4976-8a97-8d2ec4627d80">

### Summary
| Model         | Response                                                                                                                                     | Quality  | Speed    | Resource Usage |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|----------------|
| Llama 3.2     | As words flow from my restless mind, I chase the rhythm, leave it behind, A verse takes shape, a story's spun, And in the process, I am undone. | Simple   | 10.919s  | 0% CPU         |
| Mistral       | In the quiet of thought, where whispers take flight, Born from the heart's deepest depths, words ignite. A dance of syntax and rhythmic delight... | Complex  | 19.247s  | 0% CPU         |
| Phi 3 Medium  | In the dance of words and lines, I weave a tapestry so fine, With quill in hand, I craft a world where thoughts intertwine...                   | Complex  | 50.406s  | 0% CPU         |

- **Response Quality**:
  - **Llama 3.2** produced a relatively simple and concise poem. While the rhythm was clear, the complexity and depth of imagery were limited compared to the other models.
  - **Mistral** created a more intricate and descriptive poem, with a sophisticated use of language, metaphors, and structure, making it stand out for its creativity and emotional depth.
  - **Phi 3 Medium** also crafted a complex poem, similar in depth and metaphorical richness to Mistral, but with a more refined focus on poetic structure and flow.

- **Speed**:
  - **Llama 3.2** was the fastest, completing the poem generation in **10.919 seconds**. 
  - **Mistral** took nearly double the time at **19.247 seconds**, but still remained reasonably quick given the complexity of its output.
  - **Phi 3 Medium** was by far the slowest, taking **50.406 seconds** to generate its response, which may be attributed to the model's larger size and more complex generation process.

- **Resource Usage**:
  - All three models used **0% CPU** during the task, indicating minimal system resource usage despite the variation in generation times.

In summary, **Llama 3.2** is the quickest and offers simpler output, making it ideal for rapid creative tasks with less emphasis on complexity. **Mistral** strikes a balance between complexity and speed, producing high-quality, imaginative responses relatively quickly. **Phi 3 Medium**, while delivering a similarly complex response, takes much longer, which may be a consideration for tasks where speed is a priority.

# 3) Focused Experimentation
**Area of Focus**: Domain-Specific Performance (Medical)

We will ask the model to explain what a heart attack is to three different audience groups.

## a) 8-Year-Old Child
**Prompt**: Explain what a heart attack is to an 8-year-old child.

### Llama 3.2 Output
<img width="867" alt="image" src="https://github.com/user-attachments/assets/198542c3-cc72-48a8-b601-fae57b717420">

### Mistral Output
<img width="867" alt="image" src="https://github.com/user-attachments/assets/f0f9b3e9-0b8b-466e-93ba-191f01f5c6eb">

### Phi 3 Medium Output
<img width="867" alt="image" src="https://github.com/user-attachments/assets/4a252ac0-63aa-481a-9826-b52a802d6a43">

### Summary
| Model        | Response                                                                                                                                                                                                                                                   | Observation                                                                                                      |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| Llama 3.2    | So, you know how our bodies need food, water, and air to work properly? Well, one of the most important jobs that our hearts do is help send blood to all parts of our body. Sometimes, if the heart gets too sick or hurt, it can't send enough blood...      | Simple vocabulary and tries to not scare the child.                                                              |
| Mistral      | Hi there! So, imagine a heart is like a super powerful pump that keeps blood flowing to all parts of our body. Sometimes, something blocks this pump's artery (a channel inside the heart), preventing it from working properly...                               | Perhaps a little complicated for an 8-year-old but still reassures everything will be okay.                      |
| Phi 3 Medium | A heart attack happens when your body doesn't get enough blood because something’s blocking it from getting through, which can make you feel very sick or hurt really bad in the chest area. It's like a traffic jam inside your heart where cars are stuck... | Concise and uses a great example to aid the explanation.                                                         |

- **Llama 3.2**:
  - **Response**: The explanation used very simple language and relatable concepts like cutting a finger and needing stitches, which can help a child understand without feeling scared. It emphasized that there are grown-ups and medicine to help.
  - **Observation**: This model's response was very effective in using child-friendly language and avoiding overwhelming details. The tone was reassuring, making it suitable for an 8-year-old.

- **Mistral**:
  - **Response**: This explanation likened the heart to a powerful pump but introduced terms like "artery" and "blockage," which might be more complex for a young child. The response still reassured the child by focusing on doctors' ability to help after a heart attack.
  - **Observation**: While the analogy of a pump is helpful, the language may be a bit too advanced for an 8-year-old, potentially causing confusion. However, the message of reassurance remained strong, which could comfort the child.

- **Phi 3 Medium**:
  - **Response**: The explanation used a clear analogy, describing a heart attack as a "traffic jam" inside the heart, which is an accessible and relatable example for a child. It was concise and straight to the point.
  - **Observation**: This model provided the best example to aid understanding, using simple yet effective language. The "traffic jam" analogy would likely resonate well with an 8-year-old, making the concept easier to grasp.

### Overall:
- **Llama 3.2** prioritized simplicity and reassurance, making it ideal for young children who might get scared by the concept of a heart attack.
- **Mistral** used more complex terminology, which might be challenging for a child to fully understand, though it maintained a comforting tone.
- **Phi 3 Medium** offered a concise and easily understandable explanation using a "traffic jam" analogy, which is likely the most effective for helping a child visualize and comprehend the concept.

## b) High School Student
**Prompt**: Explain what a heart attack is to a high school student.

### Llama 3.2 Output
<img width="918" alt="image" src="https://github.com/user-attachments/assets/ad18244d-59d6-42eb-892a-f21d31e27dd3">

### Mistral Output
<img width="918" alt="image" src="https://github.com/user-attachments/assets/3381cf84-e85f-4cd4-a7ae-a3dd1b9baaae">

### Phi 3 Medium Output
<img width="918" alt="image" src="https://github.com/user-attachments/assets/b465425a-d77c-451a-9ca0-7996e5cc0551">

### Summary
| Model         | Response                                                                                                                                                                                                                                                   | Observation                                                                                                                |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Llama 3.2     | A heart attack, also known as myocardial infarction, occurs when the blood flow to your heart is blocked or reduced. This means that oxygen-rich blood can't reach the heart muscle, causing damage. Imagine your heart as a pipe system... | More detailed than the previous slide. Great example to ensure the concept is understood and adds a list of symptoms to be aware of. |
| Mistral       | A heart attack happens when a blockage prevents blood from reaching a section of the heart muscle, causing it to die. It's like a part of your engine not getting fuel due to a clogged pipe. Symptoms include chest pain, shortness of breath, nausea, and cold sweats... | Good example and emphasizes the need to be aware.                                                                          |
| Phi 3 Medium  | A heart attack occurs when blood flow that brings oxygen to your heart muscle gets blocked, usually by a buildup of fat, cholesterol, or plaque in the arteries (a process known as coronary artery disease). When this happens, the heart can't get enough oxygen... | Most precise so far, but no example.                                                                                     |

- **Llama 3.2**:
  - **Response**: This model provided a thorough explanation, introducing medical terminology like "myocardial infarction" while simplifying it with an analogy of a pipe system. The inclusion of symptoms such as chest pain and shortness of breath is valuable for the reader.
  - **Observation**: The detailed explanation and symptom list enhance understanding, making it effective for educating someone about heart attacks. The analogy aids in visualization, making the concept more accessible.

- **Mistral**:
  - **Response**: Mistral offered a clear explanation of how a blockage affects blood flow to the heart muscle, using an engine analogy for clarity. It also listed symptoms similar to Llama 3.2, highlighting the importance of immediate medical attention.
  - **Observation**: The response is effective and emphasizes the urgency of seeking help. While it provides a good example, it could benefit from slightly more detail on the causes and implications of a heart attack.

- **Phi 3 Medium**:
  - **Response**: This model provided a precise explanation, detailing the biological process behind a heart attack, including terms like "coronary artery disease" and the significance of oxygen flow. However, it lacked an illustrative example or analogy to aid understanding.
  - **Observation**: While the response is informative and accurate, the absence of a relatable analogy may make it less accessible for a general audience. The focus on precision is commendable but may not resonate as well with those unfamiliar with medical terminology.

### Overall:
- **Llama 3.2** excelled in clarity and detail, providing a well-rounded explanation suitable for a lay audience with its helpful analogy and symptom list.
- **Mistral** struck a balance between clarity and urgency, making it a strong choice for emphasizing the need for immediate medical help, although it could benefit from additional detail.
- **Phi 3 Medium** delivered the most precise explanation but may alienate some readers with its technical language and lack of illustrative examples, making it less approachable for individuals without a medical background.

## c) Med-School Student
**Prompt**: Explain what a heart attack is to a med-school student.

### Llama 3.2 Output
<img width="912" alt="image" src="https://github.com/user-attachments/assets/c092fdbd-fb97-4dc7-a93f-81f02f86ceda">

### Mistral Output
<img width="912" alt="image" src="https://github.com/user-attachments/assets/79afe493-ff36-4e47-933b-7134a089e11c">

### Phi 3 Medium Output
<img width="912" alt="image" src="https://github.com/user-attachments/assets/717b5704-acc5-47d3-b643-55786f5a8249">

### Summary
| Model         | Response                                                                                                                                                                                                                                                   | Observation                                                                                                                |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Llama 3.2     | A heart attack, or myocardial infarction, occurs when blood flow to the heart is severely obstructed due to: 1. Atherosclerosis (plaque buildup in coronary arteries) 2. Thrombosis (blood clot formation) 3. Vasospasm (spasm of a coronary artery)... | Very specific medical terminology. Describes the causes and effects in a way that would be meaningful to an aspiring doctor. |
| Mistral       | A heart attack (myocardial infarction) occurs when blood flow to a part of the heart is blocked, usually by a clot. This can damage or destroy part of the heart muscle. It's often caused by coronary artery atherosclerosis, where plaque builds up in the arteries... | Emphasizes the importance of having a holistic understanding.                                                              |
| Phi 3 Medium  | A heart attack, or myocardial infarction (MI), occurs when blood flow to part of the heart muscle becomes blocked, usually by a buildup of fatty deposits on the inner walls of coronary arteries which can lead to death of cardiac tissue.                    | Shortest response out of its three, despite this context implying the most complexity.                                     |

- **Llama 3.2**:
  - **Response**: This model offered a detailed and technical explanation, using specific medical terminology such as "ischemia," "necrosis," and "myocardium." It outlined the causes of a heart attack, including atherosclerosis and thrombosis, and provided information on pathophysiological mechanisms and clinical presentations.
  - **Observation**: While the response is highly informative and suitable for someone with a medical background or an aspiring doctor, the heavy use of medical jargon may be challenging for laypersons to fully grasp.

- **Mistral**:
  - **Response**: Mistral provided a clear and concise explanation of a heart attack, mentioning key causes such as blood clots and atherosclerosis. It emphasized the importance of understanding the pathophysiology, risk factors, and treatment options.
  - **Observation**: This model strikes a balance between detail and accessibility. While it covers essential information, its focus on a holistic understanding makes it a good choice for medical students or individuals seeking foundational knowledge without overwhelming complexity.

- **Phi 3 Medium**:
  - **Response**: This model gave a straightforward definition of a heart attack, identifying the blockage of blood flow and the typical cause of fatty deposits. While it is concise, it lacks the depth of explanation found in the other models.
  - **Observation**: Although the response is the shortest, it effectively conveys the basic concept. However, it may leave out important details regarding the mechanisms and clinical signs, making it less informative for those looking for a more comprehensive understanding.

### Overall:
- **Llama 3.2** excels in providing detailed, technical information, making it suitable for those with a medical background.
- **Mistral** offers a balanced approach, combining essential details with a focus on holistic understanding, making it suitable for aspiring medical professionals and laypersons alike.
- **Phi 3 Medium** delivers a concise explanation but sacrifices depth for brevity, which may not suffice for readers seeking a more thorough understanding of heart attacks.

# 4) Analysis of Strengths and Weaknesses


# 5) Insights about Open-Source LLMs


# 6) Practical Implications of Findings


# 7) Challenges I Encountered


# Conclusion











