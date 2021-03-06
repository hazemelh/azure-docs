---
title: "Quickstart: Create knowledge base - REST, Java - QnA Maker"
titleSuffix: Azure Cognitive Services
description: This Java REST-based quickstart walks you through creating a sample QnA Maker knowledge base, programmatically, that will appear in your Azure Dashboard of your Cognitive Services API account..
services: cognitive-services
author: diberry
manager: nitinme

ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: quickstart
ms.date: 08/30/2019
ms.author: diberry
---

# Quickstart: Create a knowledge base in QnA Maker using Java

This quickstart walks you through programmatically creating a sample QnA Maker knowledge base. QnA Maker automatically extracts questions and answers from semi-structured content, like FAQs, from [data sources](../Concepts/data-sources-supported.md). The model for the knowledge base is defined in the JSON sent in the body of the API request.

[!INCLUDE [Code is available in Azure-Samples GitHub repo](../../../../includes/cognitive-services-qnamaker-java-repo-note.md)]

## Create a knowledge base file

Create a file named `CreateKB.java`

## Add the required dependencies

At the top of `CreateKB.java`, add the following lines to add necessary dependencies to the project:

[!code-java[Add the required dependencies](~/samples-qnamaker-java/documentation-samples/quickstarts/create-knowledge-base/CreateKB.java?range=1-5 "Add the required dependencies")]

## Add the required constants
After the preceding required dependencies, add the required constants to the `CreateKB` class to access QnA Maker. Replace the value of the `subscriptionKey`variable with your own QnA Maker key. You do not need to add the final curly bracket to end the class; it is in the final code snippet at the end of this quickstart.

[!code-java[Add the required constants](~/samples-qnamaker-java/documentation-samples/quickstarts/create-knowledge-base/CreateKB.java?range=26-34 "Add the required constants")]


## Add the KB model definition classes
After the constants, add the following classes and functions inside the `CreateKB` class to serialize the model definition object into JSON.

[!code-java[Add the KB model definition classes](~/samples-qnamaker-java/documentation-samples/quickstarts/create-knowledge-base/CreateKB.java?range=36-80 "Add the KB model definition classes")]

## Add supporting functions

Next, add the following supporting functions inside the `CreateKB` class.

1. Add the following function to print out JSON in a readable format:

    [!code-java[Add the PrettyPrint function](~/samples-qnamaker-java/documentation-samples/quickstarts/create-knowledge-base/CreateKB.java?range=82-87 "Add the KB model definition classes")]

2. Add the following class to manage the HTTP response:

    [!code-java[Add class to manage the HTTP response](~/samples-qnamaker-java/documentation-samples/quickstarts/create-knowledge-base/CreateKB.java?range=89-97 "Add class to manage the HTTP response")]

3. Add the following method to make a POST request to the QnA Maker APIs. The `Ocp-Apim-Subscription-Key` is the QnA Maker service key, used for authentication.

    [!code-java[Add POST method](~/samples-qnamaker-java/documentation-samples/quickstarts/create-knowledge-base/CreateKB.java?range=99-121 "Add POST method")]

4. Add the following method to make a GET request to the QnA Maker APIs.

    [!code-java[Add GET method](~/samples-qnamaker-java/documentation-samples/quickstarts/create-knowledge-base/CreateKB.java?range=123-137 "Add GET method")]

## Add a method to create the KB
Add the following method to create the KB by calling into the Post method.

[!code-java[Add CreateKB method](~/samples-qnamaker-java/documentation-samples/quickstarts/create-knowledge-base/CreateKB.java?range=139-144 "Add CreateKB method")]

This API call returns a JSON response that includes the operation ID. Use the operation ID to determine if the KB is successfully created.

```JSON
{
  "operationState": "NotStarted",
  "createdTimestamp": "2018-09-26T05:19:01Z",
  "lastActionTimestamp": "2018-09-26T05:19:01Z",
  "userId": "XXX9549466094e1cb4fd063b646e1ad6",
  "operationId": "8dfb6a82-ae58-4bcb-95b7-d1239ae25681"
}
```

## Add a method to get status
Add the following method to check the creation status.

[!code-java[Add GetStatus method](~/samples-qnamaker-java/documentation-samples/quickstarts/create-knowledge-base/CreateKB.java?range=146-150 "Add GetStatus method")]

Repeat the call until success or failure:

```JSON
{
  "operationState": "Succeeded",
  "createdTimestamp": "2018-09-26T05:22:53Z",
  "lastActionTimestamp": "2018-09-26T05:23:08Z",
  "resourceLocation": "/knowledgebases/XXX7892b-10cf-47e2-a3ae-e40683adb714",
  "userId": "XXX9549466094e1cb4fd063b646e1ad6",
  "operationId": "177e12ff-5d04-4b73-b594-8575f9787963"
}
```

## Add a main method
The main method creates the KB, then polls for the status. The operation ID is returned in the POST response header field **Location**, then used as part of the route in the GET request. The `while` loop retries the status if it is not completed.

[!code-java[Add main method](~/samples-qnamaker-java/documentation-samples/quickstarts/create-knowledge-base/CreateKB.java?range=152-191 "Add main method")]

## Compile and run the program

1. Make sure the gson library is in the `./libs` directory. At the command-line, compile the file `CreateKB.java`:

    ```bash
    javac -cp ".;libs/*" CreateKB.java
    ```

2. Enter the following command at a command-line to run the program. It will send the request to the QnA Maker API to create the KB, then it will poll for the results every 30 seconds. Each response is printed to the console window.

    ```bash
    java -cp ",;libs/*" CreateKB
    ```

Once your knowledge base is created, you can view it in your QnA Maker Portal, [My knowledge bases](https://www.qnamaker.ai/Home/MyServices) page.

[!INCLUDE [Clean up files and KB](../../../../includes/cognitive-services-qnamaker-quickstart-cleanup-resources.md)]

## Next steps

> [!div class="nextstepaction"]
> [QnA Maker (V4) REST API Reference](https://go.microsoft.com/fwlink/?linkid=2092179)
