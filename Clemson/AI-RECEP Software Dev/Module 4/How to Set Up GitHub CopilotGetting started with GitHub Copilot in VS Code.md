This tutorial walks you through the key features of GitHub Copilot in Visual Studio Code. Learn how to get started with the [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot "GitHub Copilot - Visual Studio Marketplace") extension to get AI-powered code suggestions in the editor, use chat conversations to refactor your code, and fix code errors with smart actions.

**Note:** While we're using TypeScript for this tutorial, please note that Copilot is also trained on numerous other languages and a wide variety of frameworks.

For an overview of what you can do with GitHub Copilot in VS Code, see the [GitHub Copilot Overview](https://code.visualstudio.com/docs/copilot/overview "GitHub Copilot overview").

## Prerequisites

- To use GitHub Copilot in VS Code, you must have the [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot "GitHub Copilot - Visual Studio Marketplace") extension. When you install this extension, the [GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat "GitHub Copilot - Visual Studio Marketplace") extension is also installed.
    
- To use GitHub Copilot, you must have an active subscription for GitHub Copilot in your personal account, or you need to be assigned a seat by your organization.
    

Follow these steps to [set up GitHub Copilot in VS Code](https://code.visualstudio.com/docs/copilot/setup "Set up GitHub Copilot") by signing up for a subscription and installing the Copilot extension in VS Code.

## Get your first code suggestion

Now that you've signed up for Copilot and activated the extension, let's see its assistance in action!

To get started with GitHub Copilot in VS Code, you don't have to do anything special. As you're typing code in the editor, Copilot automatically presents you code suggestions in the editor to help you code more efficiently.

1. Open Visual Studio Code and create a new TypeScript file **Calculator.ts**.

2. In the TypeScript file, start typing the following class definition: **class Calculator**

Copilot automatically suggests a method for our **Calculator** class in gray dimmed text (ghost text). In our example, the **add** method is suggested. The exact suggestions can vary.

![image of Code, Calculator.ts](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/m4jYF2m-TEeifRd1GIgY3g_b7c0a6365f2546dfb30b240b758a1df1_copilot-code-completion.png?expiry=1757548800000&hmac=ppdeCKE5o4X6vGhau6q1TS8qFu6mJtXW2yLxy9plrHs)

3. To accept the suggestion, press the **Tab** key.

Congratulations! You've just accepted your first AI-powered inline suggestion. As you continue typing, Copilot updates the inline suggestion accordingly.

4. For any given input, there might be multiple suggestions. Type the following inside the class to add a **fibonacci** method:

Hover over the suggestion in the editor and notice that there are multiple suggestions.

![image showing the use of the fibonacci method and AI suggestions](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/hSeuM4j0TMKjcbbkj--wag_156c75c65c7945a8958e6d2e440253f1_copilot-code-completion-multiple.png?expiry=1757548800000&hmac=WKTBo0FqqnVPKMicHMZt9iaId7r9g4svE2_y4KcIL74)

You can use the arrow controls or use the keybindings to show the next (**Alt+]**) or previous (**Alt+[**) suggestion.

AI-powered code completions can help you with generating boilerplate or repetitive code, letting you stay in the developer flow and focus on more complex coding tasks.

## Refactor your code through AI chat

As you work on an existing codebase, you often need to refactor or improve existing code. With the [Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat "GitHub Copilot Chat - Visual Studio Marketplace") extension, you can use AI-driven chat conversations in VS Code to ask specific tasks about your code.

Let's use Copilot Chat to help us with generating and refactoring code.

**1.** First, add a new TypeScript file **server.ts** to your workspace.

Let's use the Copilot inline chat in the editor to generate a simple Express web server.

**2.** Now, press **Ctrl+I** on your keyboard to bring up Copilot inline chat.

With Copilot inline chat you get a chat interface that lets you ask questions about your code by using natural language.

![image with text box that says: "Ask Copilot to generate code"](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/-HH6YS8rR_-P-FN5PnYVdg_5359613dbf4c4141a763f6843a3d16f1_copilot-inline-chat.png?expiry=1757548800000&hmac=l1YOgnkZ6DEVVHJt53UBE-qhgZ859doUK5EHC0YLka0)

**3.** Type _"add a simple express web server"_ in the chat input field, and press **Enter** to send the chat request or prompt to Copilot.

Notice that Copilot returns a streaming response into the editor. The response is an implementation for a simple Node.js Express web server.

![image showing the AI response to "add a simple express web server"](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/uYEPunAhQkCO65ShK1YOCA_9bba06e1253a47379351a088da4accf1_copilot-inline-chat-express-server.png?expiry=1757548800000&hmac=Qztmdilmjsndcv1o3W9Q7lYTbldPy0sFPOAAL5lN4r0)

**4.** Select **Accept** or press **Ctrl+Enter** to apply the proposed code changes.

Congratulations! You've used GitHub Copilot Chat for generating code using chat and natural language.

**5.** In the editor, select the **app.get('/'**, req, res) method, and then press **Ctrl+I** to start inline chat.

By selecting a range of text in the editor, you provide more context to Copilot about your request.

**6.** Type _"return a static index.html file"_ in the chat input field, and press **Enter** to send the chat request or prompt.

Notice how Copilot updates the existing method implementation to return an **index.html** file. Optionally, select the **Show changes** button to view a diff view and compare the changes.

![image showing how to view changes made to AI code responses](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/gqZpiT_0Ta269KgJ6SM8Cg_353c0504f5fa4af5a41dc4e70d4270f1_copilot-inline-chat-refactor.png?expiry=1757548800000&hmac=7qziGDmg3c49-sPglO9Fe0HypnKgW2F9V8blPeR5mqo)

**7.** Select **Accept** or press **Ctrl+Enter** to apply the proposed code changes.

Experiment further with Copilot Chat, for example to add more routes to your web server, or ask Copilot Chat to add error handling, and more.

With Copilot Chat you can use a chat conversation and natural language to direct Copilot to perform specific tasks on your codebase. With inline chat, you can stay in the flow of coding, and ask for AI assistance in the moment, when you need it, without switching context.

## Use Copilot Chat for general programming questions

As you're working in a new codebase, or exploring a new programming language, you might have more general questions come up. GitHub Copilot Chat lets you open a chat conversation on the side, and which keeps track of the history of your questions.

**1.** Open the Chat view from the Activity Bar or press **Ctrl+Alt+I**.

![Image of the Activity Bar in GitHub Copilot](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/HQtFPgCtTJC4oxW3jyATxw_5521b20c04c44b6ca95a68c0f12f72f1_copilot-chat-view.png?expiry=1757548800000&hmac=7mFb6QVOKfS33GGjkhR3M0CnMbeBT2bwuDucx4KfeFI)

**2.** Type "what is recursion?" in the chat input field and press **Enter** to send the request to Copilot.

![image of the Chat responses on Copilot, example question is "what is recursion?"](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/L0tQu3KUTKKhsyt7bSf-gg_0948cc101cd0415da57eff425d4777f1_copilot-chat-view-recursion.png?expiry=1757548800000&hmac=QgRqGA-Q5ajZip-fIUWIV45BDdCc8K-ceykE1KRjv4s)

Notice how the chat response contains rich results, consisting of text and a code block. The code block in the chat response supports IntelliSense, which enables you get information about methods and symbols by hovering over them, or to go to their definition.

**3.** Select the title of the Chat view and drag it to the right side of the editor to dock it to the Secondary side bar.

![image showing multiple view options in Copilot, including moving the Chat tool across the screen](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/CKC61bXdTguHgeVCd97Qlg_8373861b59cc4c9dbc2e6b22754ea1f1_copilot-chat-view-secondary-side-bar.png?expiry=1757548800000&hmac=5XO0VnTi54r98dIQsFOZSwojlqd8p5bsWazS6Pmuk14)

Putting the Chat view in the Secondary side bar can be useful if you want to open another view in the Primary side bar, for example the Explorer view to navigate your workspace. Learn about [custom layouts and the Secondary side bar](https://code.visualstudio.com/docs/editor/custom-layout#__secondary-side-bar "Custom layout of Visual Studio Code").

## Fix coding errors with Copilot

Aside from inline completions and chat conversations, GitHub Copilot is available in different places and throughout your developer flow in VS Code. You might notice the presence of Copilot functionality through the _sparkle_ icon in the VS Code user interface.

One such place is the Copilot coding actions in the editor, whenever there you have a red squiggle because of a compiler error. Let's see how Copilot can help with resolving coding errors.

**1.** Open the **server.ts** TypeScript file that you created earlier in the editor.

Notice that the **import express from 'express';** statement contains a red squiggle. If you put the cursor on the red squiggle, you can see the Copilot sparkle appear.

![image showing red squiggle under "express," an example of Copilot checking for errors](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/QOBxFooNRLmhmwz7bzeTiQ_467711b2977c4e33b61156217b1309f1_copilot-code-action-sparkle.png?expiry=1757548800000&hmac=ut6mzLl7qW7f8lZ1jJc3lSCNYRvwoAA3cWcaJmfG9Co)

**2.** Select the sparkle to view the Copilot code actions, and then select **Fix using Copilot**.

![image showing option to "Fix using Copilot" on item with red squiggle error](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/CnmPVWm4Q26Qd0gY972JKg_cc253fb1164149059c2be36a6ff06cf1_copilot-code-action-fix.png?expiry=1757548800000&hmac=N-s19HrVcGdgnnfZa6mKClXUtuVtQegN32B9lRprnQc)

Notice that the second argument gets a red squiggle because the method only accepts one argument.

**3.** Notice that the Copilot inline chat comes up, prepopulated with the error message, and a solution to fix the problem.

![image showing how to use the "Insert into Terminal" tool](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/oiq_WzvtTPmDRPomqZC28Q_59c18f1544964e8f8a4a7a57fe6edcf1_copilot-code-action-fix-result.png?expiry=1757548800000&hmac=9H_dtBi0b5YuACEmzS-HmVzLb-Ho4Uu15SMDiW_dl-s)

Directly from the chat response, you can optionally select the **Insert into Terminal** button to copy the proposed command in your terminal.

## Congratulations

Congratulations, you've now used artificial intelligence to enhance your coding! In this tutorial, you successfully set up Copilot in VS Code, and used Copilot code completions, Copilot Chat, and code actions to help you code more efficiently.

You've started experimenting with Copilot and there's a lot more you can do with it! To learn more about GitHub Copilot Chat, proceed to the [Copilot Chat Tutorial](https://code.visualstudio.com/docs/copilot/getting-started-chat "Getting started with GitHub Copilot Chat in VS Code").

_To view this article in its original formatting on the Visual Studio Code website,_ [_click here_](https://code.visualstudio.com/docs/copilot/getting-started "Getting started with GitHub Copilot in VS Code")_._