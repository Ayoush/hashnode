## Elixir Dynamic Queries Made Simple

Okay so before we address the elephant in the room I would like to share the case statement which forces me to look for Dynamic Queries the very first hand.

> So in our project, I was asked to create a search filter that will take either `user_ids` or `project_ids` or `both`, and depending upon this input an appropriate SQL query should be formed.

> There are two ways of doing this:-
1. One to perform queries that will be returned based on the parameters that will be passed by the user. In this case, I need to put a conditional statement on params.
2. The Second one is using Dynamic Query which we are going to learn in this post using the same case statement that I mentioned above.

Here is a glimpse of “Database Relation” which might help you imagine.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663133653978/iopwKab1l.png align="left")

So enough of the foreplay now let’s dive directly into the topic.

So taking reference to the above diagram if I have to fetch a task for a user or for a group of users and then filter them out in a particular project or in a group of projects then first I have to put a join on different tables which is basically what I did while composing this query.

%[https://gist.github.com/Ayoush/7529ca04440f2e1e7379045be00a04f4#file-example-ex]

Basic stuff right? But the real fun begins in the 6th line where we are directing our query to a function where the magic is going to happen.

Before that I want to share one important thing **Always remember the sequence**. What actually I am referring with this is the sequence in which you have joined you table. To help you understand more clearly here is one more diagram.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663134258904/qgFIIm5EB.png align="left")

So the `params` that we are passing in the `filter_for_tasks_for_criteria` will have the joins in this sequence only.

Now the function of the hour `filter_for_tasks_for_criteria`.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663134330343/pzs4dC6dj.png align="left")

I know there are a lot of things to process here but I will break it down step by step.

So let’s start with the `dynamic(true)` thing that we are passing in Enum reduce function. That is the dynamic thing that will accommodate all the subsequent dynamic queries which will pass the given condition.

`{“user_ids”, user_ids}` this is the uncertain parameter that might or might not pass by the user but in case it did we will look into the joins`(look at the sequence closely)` and add it to our dynamic query.

The same thing goes for `project_ids` and `workspace_id`.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663134384267/iaRAoQUb-.png align="left")

If you look closely at the encircled part, that is by far the most important line which is actually making it work. So it basically means if none of the conditions matches simply return the dynamic query that we have assembled till now and if you haven't put it there, it won’t return the query.

So with this, I think I have explained whatever little I know or experienced while working on the elixir.

If you really like the blog show some love and follow or a clap would just do fine.

Happy coding, until next time.



