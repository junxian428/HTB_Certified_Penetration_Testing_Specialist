<h3>The Concept of Attacks</h3>

To effectively understand attacks on the different services, we should look at how these services can be attacked. A concept is an outlined plan that is applied to future projects. As an example, we can think of the concept of building a house. Many houses have a basement, four walls, and a roof. Most homes are built this way, and it is a concept that is applied all over the world. The finer details, such as the material used or the type of design, are flexible and can be adapted to individual wishes and circumstances. This example shows that a concept needs a general categorization (floor, walls, roof).

In our case, we need to create a concept for the attacks on all possible services and divide it into categories that summarize all services but leave the individual attack methods.

To explain a little more clearly what we are talking about here, we can try to group the services SSH, FTP, SMB, and HTTP ourselves and figure out what these services have in common. Then we need to create a structure that will allow us to identify the attack points of these different services using a single pattern.

Analyzing commonalities and creating pattern templates that fit all conceivable cases is not a finished product but rather a process that makes these pattern templates grow larger and larger. Therefore, we have created a pattern template for this topic for you to better and more efficiently teach and explain the concept behind the attacks.

<h3>The Concept of Attacks</h3>

<img width="633" height="341" alt="image" src="https://github.com/user-attachments/assets/a8c5265e-4c32-4bff-9a17-a0a40f2f9f62" />

The concept is based on four categories that occur for each vulnerability. First, we have a Source that performs the specific request to a Process where the vulnerability gets triggered. Each process has a specific set of Privileges with which it is executed. Each process has a task with a specific goal or Destination to either compute new data or forward it. However, the individual and unique specifications under these categories may differ from service to service.

Every task and piece of information follows a specific pattern, a cycle, which we have deliberately made linear. This is because the Destination does not always serve as a Source and is therefore not treated as a source of a new task.

For any task to come into existence at all, it needs an idea, information (Source), a planned process for it (Processes), and a specific goal (Destination) to be achieved. Therefore, the category of Privileges is necessary to control information processing appropriately.
