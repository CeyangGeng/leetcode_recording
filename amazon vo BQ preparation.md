# amazon vo BQ

1. ```
   Q:问没有足够数据时候如何做的决定:(list several plans)
   A: Here I want to talk about my first project called the faceshifter which chould add Peking opera facial mask to human face. This project is cooperated with a very popular TV series promotion. I took ownership of this project because I like this TV series a lot and if this application can be well developed, it can greatly benefit the TV series promotion. The first problem to be solved is which kind of service I should implement, synchronous or asynchronous. Since I have no previous experience and my mentor did not developed this application before either. Finally, I chose the synchrounous mode because synchronous web service makes customer waiting time shorter comparing with the asynchronous mode. Besides, although the less processing time need more computing resources, I think the benefit of the customer satisefaction is much larger than the cost of computing resources.
   ```

2. ```
   Q: Tell me about your current role?
   A: I use the tornado to implement the backend part including listening to the request, parsing the parameters, calling the AI aogorithm to handle the request and returning the process result to the customers directly or by calling back. During the development, I need to cooperate closely with the sevice caller. I care a lot about their needs like the required service response time, their favorite call back format and 
   Another job is the AI model optimization using the intel toolkit called the openvino. You can use any deep learning frameword to train the model. After training, you can turned the framework into several format that openvino supports. As for the optimization, there might be some layers like drop out layer during the training but useless while inferring. The optimizer of openvino will remove these redundant layers. Besides, if a group of operations can be represented as a single mathematical operation, and thus a single node in the graph, the model optimizer will replaces this group of operation nodes with the only one operation. All these optimization will decrease the infer time greatly.
   ```

3. ```
   Q:simplify 难的问题的经验
   A: To simplify the hard problem, I think we should break it into small chunks ,list the difficult or unclear part and learn to explore these parts. Here I want to talk about one of my model optimization job. I was required to optimize this application. This application is huge. I split into three modules, the first module is to prefilter the good frames and bad frames. After this prefilter, we only need to process the bad pictures in the second module to extract the sensitive labels. The function of the third module is to match the label with the position on the picture. These three module use different frameworks including the tensorflow, pytorch and keras. So I optimize these three parts separately. Besides, I was not very familiar with the pytorch framework and the resnet50 model backbone of the second module at the beginning. So I Googled a lot of related material, read the source code of the resnet50 model and the new added pooling layer to analyze the topology of this model. I also raised questions on the stackoverflow forum for help. After about three days, I finished this optimization job within the required time.
   ```

4. ```
   Q: a project that you took initiative
   A: I initiate a project which could simplify the development process. This project makes the packaging of algorithms semi-automated. Packaging means turn the AI algorithms into AI web services. Previously, we need to start coding from blank. After finishing several such projects, I realize that the workflow of the packaging are quite similar. So I propose that we can make this packaging to be semi-automatic, some repeated code should be genreated automatically. Although it is not possible to make the packaging to be completely automatic, the semi-automatic will greatly decrease the code amount for the developer, thus accelerating the development progress.
   This semi-automatic optimization could genreate the code of running the service code in the child process, listening the customer request and testing the service. I think this project is very meaningful because it saved a lot of repeated work.
   ```

5. ```
   Q:a time that you didn't meet the deadline
   A: I did miss a deadline because I underestimated the difficulty of the task inserted midway. When I was doing a project, my mentor asked me if I could help finish another higher priority task. After understanding the requirements of the task, I thought the work load is not so heavy, I just need to update the algorithm version, change the return data format and rewrite the service wiki. So I agreed to help. But after begin working on the inserted task, I found that there are much more work than I thought. It took me 2 more days to finish the higher priority task. Thus I didn't have enough time to finish the origin task. When I realize I will miss the deadline, I calculated that I need two more days to finish the origin task.I apologized to the client immediately and asked if we could have an extended deliver date. Luckily, the customer agreed and showed understanding. I worked a lot of overtime and finished the original task with two more days. I learned that we need to estimate the difficulty correctly and do not get a conclusion without through understanding. Before agreeing to help, we should make sure that it will not delay your progress. 
   ```

6. ```
   Q: why amazon?
   A: motto and vision; technology to create fantastic shoppint experience; working environment with challenges
   ```

7. ```
    Q: Tell me about a time you disagreed with a team member
    A: Once I cooperated with one of collegues to optimize a optical character recoginition web application using the openvino inference engine. The input pictures are of random size. However, the inference engine could only accept fixed size input not flexible size. My colleague thought that we only need to resize all the pictures into the one standard size. I insist that we need to develop multiple image size standards but not one standard because if a very small picture be resized to a large fixed size, there will be a lot of unnecessay computing which will waste a lot of computing resources. My collegue thought that multiple standards will bring much more code amount and there is no need to pay that much effort. So we turned to my mentor. My mentor said that my opinion is right, we should resize the picture to their cloest standard size. After that experience, I learned that we need to insis on the high standards even we need to put into a lot of effort.
   ```

8. ```
   In addition to my technical background, I'm very creative and quickthinking. I also have very strong learning and logical thinking ability which could be reflected in my mathematical related competition awards. I am a person who respect hard-working and cares a lot about the user experience which could firmly obssess the customers. Every time I develop an AI service, I will ask the service caller about their longest waiting time that can be tolerated, their favorite call back format and if there are some additional index that they want to add to this service.
   ```

9. ```
   Q: The biggest mistake you made and what did you learn from it?/ details
   A: Here I want to talk about my project called the terror check which could detect some sensitive labels in pictures. After seeing the service wiki, I thought I just need to mark all the pictures with sensitive labels as bad pictures. After finishing the development of this service, I submit the test requirement to the testing group. It turned out that many pictures were incorrectly marked. After talking with the product manager, I found that I neglected some details that if a picture with a natinal flag located at the bottom right corner and no larger than a given size, this picture should be classified as good pictures. I apologized to the product manager immediately and corrected the mistake very soon. After this experience, I realized that before starting the development, in addition to the whole map, we should also dive deep and pay attention to the details.
   ```

10. ```
    Q: took a risk or do not have much time to make a decision/ tough decision
    A: Here I want to talk about one of my summer course project called cache lab. we need to allocate the heap memory dynamically and we should try to maximize the cache operation throuput and space utilization. To maximize and compromize between these two parameters, we could use the tree or the segregated linked list datastructures. I just know that these two methods could both meet the requirement. But I don't know which one is better. Although I want to ranked high on the score board, I have not much time to tangle in these two methods. So I picked the segregated free list to finish my assignment. In the end, I got great grades with this method. Sometimes, there is no need to spend a lot of time making decisions, just pick one and get started. Action is the most important thing.
    ```

11. ```
    Q: challenge from customers
    A: Here I want to talk about one of projects which could extract the label from TV series line. The clients could use these label to recomend commercial products to the audience. Initially, the client told me that I should develop this service in syncronous mode because they have not much requirement on the response time. After finishing the development, the client found that the response of syncronous mode is out of their tolerance and I should change the service into syncronous mode. To make the clients satisefied, I rewrote all the code to meet the requirement of the clients. It turned out the syncronous mode is right, and the service is still be in use with its good service parameters. Although the change of requirement added a lot of extra work to me, but the customer obsession is much more important.
    ```

12. ```
    Q: negative feedback
    A: The first time I was assigned a model optimization work, I proceed very slow because I am not very familiar with the openvno toolkit. I was afraid of making mistake during the optimization. The first few days I just read the documentation and try to understand all of the toolkit functions thourouly. My mentor said that my progress is too slow and it is not right to begin only after having the full understanding of all the functions. I just need to understand the critical and relavant part of this assigned project. Reading and understanding is far from enough, the key point is to begin practice. With his suggestion, I optimized the model while learning. After this experience, I learned that action is much important than just thinking in mind.
    ```

13. ```
    Q: sacrifice short for long goal
    A: 
    ```

14. ```
    Q: out of responsibility
    A: There was one time when I was assigned to finish a task with another intern. We were responsible for different parts. He has never used the pytorch framework before and not familiar with the transition from the pytorch framework to the onnx framework. I have experience in this filed. When he came tome, I walked through the whole work flow step by step with him, evaluate all the code he had written and brought up a lot of opinions but not just said it is not my job. With my suggestion, he solved the problem successfully. I also achieved a great sense of achievement. 
    ```

15. ```
    Q: take action to help team
    A: 
    ```

16. ```
    Q: get out of comfort zone
    A: 
    ```

17. ```
    Q: simple solution 
    ```

18. ```
    Q: Dive deep
    A: In my recent model optimization work I came across a problem saying that there is a dynamic input layer in the model. To find out this node, I read the source code of the resnet50 model backbone to findout the topologies of this network, but I didn't find where did the problem came from. So I came into the error file and printed the all the nodes. After compling, I found that the print is stopped at a node from a customized average pooling layer which is located behind the resnet50 backbone. I knew that the problem is due to this layer. So I read the source code of this customized layer and found that the input is not a constant but a variable. So I changed the input of this layer to be a fixed constant. After this modification, I implemented the optimization successfully.
    ```

19. ```pyhon
    Q: What’d you do after you realized you couldn’t hit the date?
    A: “I looked at the features, and picked out a few I felt we could cut. The product manager agreed on a couple. Then, as bad as it sounds, I convinced QA to cut a week off the testing schedule. It was risky, but it was so important to hit the holidays. I figured we could test everything important, and it was the only way to get out in time.”
    ```

    



