Instantiation Operations

	Software development organizations continually seek to improve their software development and maintenance processes, since the latter are directly related to the quality of the resulting software products. Software processes are also considered important players for the software development industry, as they orchestrate activities, people and information involved in software development. Using software processes to support software development, involves instantiating concepts from the software process domain into concepts of the software project domain. In this sense, process instantiation bridges the gap between software process and software project, and, if not executed with proper assistance, may increase the distance between them, making it difficult to reconcile them. This technical report introduces a set of instantiation operations such as link, split, and merge, that allow to explicitly map software project and process elements. Instantiation operations aim to foster a smooth transition between process and project, by means of a tracing mechanism that allows the reconciliation of both perspectives. The tracing mechanism creates links between the process and project perspectives, through a structure mapping structure between the elements used to model the software process and the elements used to execute the software projects, reducing the distance between them. In this way, this mapping supports the extraction of knowledge about the processes from the event logs generated during the software development projects.
We introduce herein a set of instantiation operations to represent the mapping relationship between concepts found at the process perspective, to concepts found at the project perspective, thus allowing process and project reconciliation.


Table 1 Instantiation Operations
Name
Descritption
Link 

Establishes a link between one process activity and a single task of the project plan. The task must have the same name as the associated process activity.
Detail

Establishes a link between one process activity and a single task in the project plan. The task name must be more detailed than the activity name, but with the same meaning. 
Rename

Establishes a link between one process activity and a single task in the project plan. The task name must be different from the associated process activity name.
Case
 
Establishes a link between each activity of a process instance and the tasks in the project plan. Each task name must be more detailed than the activity name. All the tasks will be associated to an instance of the process.
Split

Establishes a link between a process activity and two or more tasks in the project plan.
Split Iteration

Establishes a link between  a process activity and two or more tasks in the project plan and distribute them across multiple iterations. This operation applies to the situation in which you want to create  two or more tasks in the project plan to one activity foreseen in the defined software process distributed  across multiple iterations.
Merge

Merges two or more process activities into a single task in the project plan and establishes a link between them.
Add

A task in the project plan has no corresponding activity in the process model.
Remove

A task in the project model has no corresponding activity in the project plan.
Link Artifact
Establishes a link between an artifact associated with a process activity and an artifact produced by a task of the project plan. The artifact produced by a task must have the same type as the artifact associated process activity.
Link Role
Establishes a link between an role associated with a process activity and an actor responsible by a task of the project plan.
	
	Each operation will be presented in detail below.


2.1 Detailed Description of Instantiation Operations

	We describe the instantiation operations with the following structure, based on the description format of Design Patterns (Gamma et al. (1995)). 

Table 2 Format for Description of each Instantiation Operation
Name
[Operation Name]
Operation
[Representation of the operation]
Description
[What does the operation do?
What type of problem does it solve?]
Motivation
[A scenario that illustrates the problem and how the behavior of each operation solves the problem of the example scenario.]
Applicability
[It is intended to describe by means of answers to the following questions:
What are the situations in which the operation can be applied?
What are the examples of situations the operation can handle?
How can you recognize the applicability situations?]
Participants
[Explanation of each element of the conceptual model involved in the implementation of the operation.]
Relationship
[Type of relationship between participants involved]
[one for one, one for many and many for one]
Pseudocode
[Pseudocode of operation operation.]
Example
SIGA-EPCT Project
[Figure that exemplifies the application of the operation.]

	Each operation is described in detail in the following subsections, using the structure shown in Table 2.

2.1.1 Link Operation

Name
	Link 

Operation
	task.createLink(iteration: Iteration, instance: Instance, project: Project, 	processActivity: Activity)

Description
	Establishes a link between one process activity and a single task of the project plan. The task must have the same name as the associated process activity. 

Motivation
	Software process activities defined for the project are instantiated, but the lack of mapping between the process and the project plan makes it difficult to extract information from the process. Creating tasks with the same name as the corresponding activity, helps reducing the gap. 

Applicability
	This operation applies to the situation in which you want to create a task in the project plan equal to the activity foreseen in the defined software process. In this situation, the foreseen activity meets the needs in its description and purpose. This operation creates a task in the project plan with the same process activity name and records the activity of the reference process.

Participants
	Activity:  Software process activity defined for the projecto
	Task: Project task present in the project plan

Relationship 
	one to one between Activity and Task.

Pseudocode
function task.createLink (iteration: Iteration, instance: Instance, 
project: Project, processActivity: Activity)
begin
    self.iteration = iteration
    self.instance = instance
    self.project = project
    self.processActivity = processActivity
    self.name = processActivity.name
    self.defineTask(task_description, task_status,  task_startDateForeseen, 
    task_startDate, task_endtDateForeseen, task_endDate)

    return task
end


Example
	Project SIGA-EPCT-EPCT
Figure 1. Example of Link Operation 

2.1.2 Detail Operation

Name
	Detail 

Operation
	task.createDetail(iteration: Iteration, instance: Instance, project: Project, 	processActivity: Activity, task_name_detail: String)
 
Description
	Establishes a link between one process activity and a single task in the project plan. The task name must be more detailed than the activity name, but with the same meaning. 

Motivation
	The activities foreseen in the software process can be defined at a high level, requiring a greater detail in its instantiation in the software project. Creating tasks, with the most detailed activity name, and representing the associated process activity for each project plan task, helps reducing the gap between process and project. 

Applicability
	This operation applies to the situation in which you want to instantiate an activity of the software process, but in the context of the software project, the task to be created must have the name of the most detailed planned activity. In this situation, the foreseen activity meets the needs in its description and purpose, being necessary a greater detailling. This operation creates a task in the project plan with the name more detailed than the name of the process activity, but with the same meaning, and records the activity of the reference process.

Participants
	Activity: Software process activity defined for the project and 
	Task: Project task present in the project plan.

Relationship 
	One to one between Activity and Task.

Pseudocode
function task.createLink (iteration: Iteration, instance: Instance, 
project: Project, processActivity: Activity, task_name_detail: String)
begin
    self.iteration = iteration
    self.instance = instance
    self.project = project
    self.processActivity = processActivity
    self.name = processActivity.name + task_name_detail
    self.defineTask(task_description, task_status, task_startDateForeseen, 
    task_startDate, task_endtDateForeseen, task_endDate)

    return task
end

Example
	SIGA-EPCT Project
Figure 2. Example of Detail Operation 

2.1.3 Rename Operation

Name
	Rename

Operation
	task.createRename(iteration: Iteration, instance: Instance, project: Project, 	processActivity: Activity, task_name: String)

Description
	Establishes a link between one process activity and a single task in the project plan. The task name must be different from the associated process activity name..


Motivation
	The activities foreseen in the software process can be defined at a high level and do not describe specifically what is intended to be accomplished in the project task, and it is necessary to rename them in their instantiation in the software project. Creating tasks, with a different name from the associated activity to fit the project context and representing the associated process activity for each project plan task, helps reducing the gap between process and project

Applicability
	This operation applies to the situation in which you want to instantiate an activity of the software process, but in the context of the software project, the task to be created must have the different name. In this situation, the foreseen activity meets the needs in its purpose, however the task name must reflect more specifically what will be accomplished, being necessary to define a different name of the associated process activity. This operation creates a task in the project plan with the task name different from the process activity name, and records the activity of the reference process.

Participants
	Activity: Software process activity defined for the project and 
	Task: Project task present in the project plan.

Relationship 
	One to one between Activity and Task.

Pseudocode
function task.createLink (iteration: Iteration, instance: Instance, 
project: Project, processActivity: Activity, task_name: String)
begin
    self.iteration = iteration
    self.instance = instance
    self.project = project
    self.processActivity = processActivity
    self.name = task_name
    self.defineTask(task_description, task_status, task_startDateForeseen, 
    task_startDate, task_endtDateForeseen, task_endDate)

    return task
end

Example
SIGA-EPCT Project
Figure 3. Example of Rename  Operation

2.1.4 Case Operation 

Name
	Case

Operation
	task.createCase(instance: Instance, project: Project, process_activities: Array)

Description
	Establishes a link between each activity of a process instance and the tasks in the project plan. Each task name must be more detailed than the activity name. All the tasks will be associated to an instance of the process.

Motivation
	The software process prescribes a set of activities that must be instantiated in the context of a software project. Creating tasks, with the most detailed activity name, for each activity foreseen in a given process instance, and representing the associated process activity for each project plan task, helps reducing the gap between process and project..

Applicability
	 This operation applies to the situation in which you want to instantiate all activities foreseen for a given instance of the software process. In this situation, the foreseen activity meets the needs in their purposes. This operation creates a task in the project plan, for each activity foreseen in the process instance, and records the defined process activity.

Participants
	Activity: Software process activity defined for the project and 
	Task: Project task present in the project plan.

Relationship 
	One to one between Activity and Task.

Pseudocode
function create_case (instance: Instance, project: Project, process_activities: Array)
begin
      for each activity in process_activities
      begin
         self.instance = instance
         self.project = project
         self.process_activity = process_activity
         self.iteration = read_iteration()
         self.name = process_activity.name + read_task_name_detail()
         self.defineTask(task_description, task_status, task_startDateForeseen, 
            task_startDate, task_endtDateForeseen, task_endDate)
         return task
     
end


Example
	SIGA-EPCT Project

Figure 4. Example of Case Operation 

2.1.5 Split Operation 

Name
	Split

Operation
	task.createSplit(iteration: Iteration, instance: Instance, project: Project, 	processActivity: Activity, task_name: String)

Description
	Establishes a link between a process activity and two or more tasks in the project plan. The task name must be different from the associated process activity name.

Motivation
	The activities foreseen in the software process can be defined at a high level, but in instantiation, it may be necessary to create two or more tasks in the project plan, in the same iteration. Creating tasks, with the most appropriate name for the software project context, and representing the associated process activity for each project plan task, helps reducing the gap between process and project. 

Applicability
	This operation applies to the situation in which you want to create two or more tasks in the project plan, in the same iteration, arising from a single activity foreseen in the defined software process. In this situation, the foreseen activity meets the needs in its description and purpose, but the high level of definition of it and the context of the project, imply the creation of more specific tasks. This operation creates two or more tasks in the project plan, in the same iteration, and records the activity of the reference process in each task created.

Participants
	Activity: Software process activity defined for the project and 
	Task: Project task present in the project plan.

Relationship 
	One to many between Activity and Task.

Pseudocode
function create_split (instance: Instance, iteration: Iteration, project: Project, process_activity: Activity, task_name: String)
begin
      while
      begin
          self.instance = instance
          self.iteration = iteration
          self.project = project
          self.process_activity = process_activity
          self.name = task_name
          self.defineTask(task_description, task_status,  task_startDateForeseen, 
            task_startDate, task_endtDateForeseen, task_endDate)
          return task
      end
end 


Example
	SIGA-EPCT Project
Figure 5. Example of Split Operation

2.1.6 Split Iteration Operation

Name
	Split Iteration

Operation
	task.createSplit(iteration: Iteration, instance: Instance, project: Project, 	processActivity: Activity, task_name: String)

Description
	Establishes a link between a process activity and two or more tasks in the project plan and distribute them across multiple iterations. This operation applies to the situation in which you want to create  two or more tasks in the project plan to one activity foreseen in the defined software process distributed across multiple iterations.

Motivation
	The activities foreseen in the software process can be defined at a high level, but in instantiation, it may be necessary to create two or more tasks in the project plan, in the different iterations. Creating tasks, with the most appropriate name for the software project context, and representing the associated process activity for each project plan task, helps reducing the gap between process and project. 

Applicability
	This operation applies to the situation in which you want to create two or more tasks in the project plan, in the different iterations, arising from a single activity foreseen in the defined software process. In this situation, the foreseen activity meets the needs in its description and purpose, but the high level of definition of it and the context of the project, imply the creation of more specific tasks. This operation creates two or more tasks in the project plan, in the different iterations, and records the activity of the reference process in each task created.. 

Participants
	Activity: Software process activity defined for the project and 
	Task: Project task present in the project plan.

Relationship 
	One to many between Activity and Task.

Pseudocode

function createSplitIteration (instance: Instance, iteration: Iteration, project: Project process_activity: Activity, task_name: String)
begin
      while
      begin
          self.iteration = read_iteration()
          self.instance = instance
          self.project = project
          self.process_activity = process_activity
          self.name = task_name
          self.defineTask(task_description, task_status,  task_startDateForeseen, 
    task_startDate, task_endtDateForeseen, , task_endDate)
          return task
      end
end

Example
	SIGA-EPCT Project
Figure 6. Example of Split Iteration  Operation

2.1.7 Merge Operation

Name
	Merge 

Operation
	task.createMerge(iteration: Iteration, instance: Instance, project: Project, process_activities: Array, task_name: String)

Description
	Merges two or more process activities into a single task in the project plan and establishes a link between them.

Motivation
	The activities foreseen in the software process can be defined at a low level, but in instantiation, it may be necessary to merge them into one task in the project plan. Creating a single task with a different name from associated activities,  in order to fit the context of the project, and representing the associated process activities to project plan task, helps reducing the gap between process and project. 

Applicability
	This operation applies to the situation in which you want to create a task in the project plan for two or more activities foreseen in the defined software process. In this situation, the foreseen activities meet the needs in its description and purpose, but for the context of the software project a single task must be created. This operation creates a task in the project plan with the most appropriate name for the software project context, and records the activities of the reference process

Participants
	Activity: Software process activity defined for the project.
	Task: Project task present in the project plan.

Relationship 
	Many to one between Activity and Task

Pseudocode

function createMerge(iteration: Iteration, instance: Instance, project: Project, process_activities: Array, task_name: String)
begin
      self.instance = instance
      self.iteration = iteration
      self.project = project
      self.process_activities = process_activities
      self.name = task_name
      self.defineTask(task_description, task_status,  task_startDateForeseen, 
    task_startDate, task_endtDateForeseen, , task_endDate)  
      return task
end

Example
	SIGA-EPCT Project

Figure 7. Example of Merge Operation

2.1.8 Add Operation

Name
	Add 

Operation
	task.createAdd(iteration: Iteration, instance: Instance, project: Project, 	task_name: String)

Description
	A task in the project plan has no corresponding activity in the process model. 


Motivation
	The activities foreseen in the software process do not meet the needs of a project plan task. A task is created and does not have the associated process activity representation.

Applicability
	This operation applies to the situation in which no software process activity meets the task in the project plan. In this situation, no foreseen activity meets the needs in its description and purpose, being necessary to create a task in the project plan without associated process activity. This operation creates a task in the project plan, and no records the activity of the reference process.

Participants
	Task: Project task present in the project plan.

Relationship 
	Not applicable.

Pseudocode
function task.createAdd(iteration: Iteration, instance: Instance, 
project: Project,, task_name: String)
begin
      self.iteration = iteration
      self.instance = instance
      self.project = project
      self.process_activity = NULL
      self.name = task_name
      self.defineTask(task_description, task_status,  task_startDateForeseen, 
    task_startDate, task_endtDateForeseen, , task_endDate)
      return task
end



Example
SIGA-EPCT Project
Figure 8. Example of Add  Operation

2.1.9 Remove Operation

Name
	Remove 

Operation
	task.remove(processActivity)

Description
	A task in the project model has no corresponding activity in the project plan.

Motivation
	The activities foreseen in the software process may not be instantiated in the software project. No task is associated with foreseen activities.

Applicability
	This operation applies to the situation in which you do not intend to create tasks for a given activity foreseen in the software process. In this situation, the foreseen activity not meets the needs in its description and purpose, and is not associated with tasks in the project plan.

Participants
	Activity: Software process activity defined for the project.

Relationship 
	Not applicable.

Pseudocode
	Not applicable.

Example
SIGA-EPCT Project
	
Figure 10. Example of Remove Operation
2.1.10 Link Artifact Operation

Name
	Link Artifact

Operation
	task.createLinkArtifact(artifact: Artifact, project: Project, processActivity: Activity)

Description
	Establishes a link between an artifact associated with a process activity and an artifact produced by a task of the project plan. The artifact produced by a task must have the same type as the artifact associated process activity.

Participants
	Artifact: Artifact associated with a defined  software process activity for the project
	TaskArtifact: Artifact associated with a project task present in the project plan

Relationship 
	One to onte between Artifact e TaskArtifact.

Pseudocode
	Not applicable.

2.1.11 Link Role  Operation

Nome
	Link Role 

Operation
	task.createLinkRole(role:  Role, project: Project,  processActivity: Activity)

Description
	Establishes a link between an role associated with a process activity and an actor responsible by a task of the project plan.

Participants
	Role: Role responsible for the activity of the software process defined for the project.
	TaskActor: Actor responsible for a project task present in the project plan

Relationship 
	One to one between Role and TaskActor.

Pseudocode
	Not applicable.


References
