---
title: 'Set a dto session key when calling WCF proxy'
description: How to handle all DTOs by setting a session key before sending to WCF host using expression lambda
comments: true
categories:
  - Development
  - .NET
tags:
  - csharp
  - dotnet
  - tutorial
fullview: true
last_modified_at: 2022-01-23 01:10:00 +0100
published: true
---

The power of the following method is avoid implementing the WCF contract client in the client side and duplicate the code for each call.
Using Reflections and Expression Lambda to handle each message before send it.
The follwing code has 3 steps specified by regions :

- Update the DTO.
- Initilialize the proxy if the channel is in status Faulted.
- Invoke the contract operation

```csharp
public static Task<RequestResponse> SendRequestAsync(Expression<Func<IUiContract, Task<RequestResponse>>> expression)
        {
            #region Set Session Key

            var call = expression.Body as MethodCallExpression;
            if (call != null)
            {
                var argument = call.Arguments[0];
                if (argument != null)
                {
                    LambdaExpression lambda = Expression.Lambda(argument, expression.Parameters);
                    Delegate d = lambda.Compile();
                    var dto = d.DynamicInvoke(new object[1]) as RequestDTO;
                    if (dto != null)
                    {
                        dto.SessionKey = ClientSession.GetSessionKey();
                    }
                }
            }

            #endregion

            #region Initialize Proxy if Faulted

            // ReSharper disable once PossibleNullReferenceException
            if ((Instance._proxy as ICommunicationObject).State == CommunicationState.Faulted)
                Instance.InitializeProxy();

            #endregion

            var func = expression.Compile();
            return func.Invoke(Instance._proxy);
        }
```

### Call the method from another class code:

```csharp
  ServiceClient.SendRequestAsync(contract => contract.AddUserAsync(dto));
````

