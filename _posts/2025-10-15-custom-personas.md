---
layout: post
title: Custom personas in GitHub Copilot
tags: [Copilot]
---
I talked about [Custom Instructions](https://mattvsts.github.io/2025/09/17/custom-copilot-chat/) in the past, but can we go further?

You can build your own persona to pair with when using GitHub Copilot. Think about specific, role-defined activities you need to perform on the regular, which would benefit from a _specialist_ rather than a generic approach Copilot could have.

Enter [Custom Chat Modes](https://code.visualstudio.com/docs/copilot/customization/custom-chat-modes#_custom-chat-modes). This is different from the custom command, and it will extend the Modes (think Ask, Edit, Agent) you have in your IDE.

![](/images/posts/2025-10-15-18-39-35.png)

![](/images/posts/2025-10-15-18-40-03.png)

This is where you build your prompt. Be specific, detailed and ensure you cover the behavior you need:

![](/images/posts/2025-10-15-18-41-28.png)

Now, there is a lot more you can do. First of all, you can select the MCP tools you want to add (in this example I used all the built-in ones). Crucially, you can also specify the model you want to use. 

![](/images/posts/2025-10-15-21-49-00.png)

Once done you can save it in the `.github/chatmodes` folder, using a `<persona>.chatmode.md` name". This will load it up in Visual Studio Code:

![](/images/posts/2025-10-15-21-49-31.png)

Let's test it!

![](/images/posts/2025-10-15-21-49-50.png)

![](/images/posts/2025-10-15-21-50-34.png)

You can build as many Personas as you need, and having specialised assistants really goes a long way in a GenAI-augmented developer experience.