# Task Manager Application

## Description
The **Task Manager Application** is designed to simplify the process of organizing and managing your daily tasks. It allows users to create, update, and delete tasks with ease, all in one centralized place. The application ensures that you stay on top of your schedule, categorizing tasks by type (e.g., personal, sport, family), and giving you control over when tasks start and end. You can manage your tasks for any day of the week, and the app will persist changes both locally and on a server for seamless access across devices.

## Domain Details
The application is centered around managing **Task** entities. Below are the fields that each task will contain, along with a description of each:

- **Task ID** (integer): A unique identifier for each task.
- **Title** (string): A short description or title of the task.
- **Start Time** (datetime): The exact time when the task is scheduled to begin.
- **End Time** (datetime): The time when the task is expected to end.
- **Task Type** (string): A category for the task (e.g., personal, sport, family, work).
- **Description** (string, optional): Additional details or notes about the task.
- **Day** (enum: Monday-Sunday): The day of the week the task is assigned to.
- **Status** (enum: Pending, In Progress, Completed): The current state of the task.

## CRUD Operations

### 1. **Create**
   - **Description**: Users can create new tasks by providing necessary details (title, start and end time, type, etc.). The task is immediately saved to the local database.
   - **Steps**:
     1. User inputs task details.
     2. The task is assigned a unique ID.
     3. Task data is stored in the local database and, if online, sent to the server.
     4. Response is given to the user confirming task creation.

### 2. **Read**
   - **Description**: Users can view all tasks scheduled for any specific day or filter by task type, status, or other fields.
   - **Steps**:
     1. The user selects a specific day or filter option.
     2. The application retrieves task data from the local database and, if online, syncs with the server for any updated tasks.
     3. Tasks are displayed to the user in a list or calendar view.

### 3. **Update**
   - **Description**: Users can edit the details of an existing task, including changing the start and end times, task type, or status.
   - **Steps**:
     1. The user selects a task to update.
     2. The task's existing details are pre-populated in an update form.
     3. User edits the desired fields and submits the changes.
     4. Task data is updated in the local database and, if online, the changes are synced with the server.

### 4. **Delete**
   - **Description**: Users can delete tasks they no longer want to keep.
   - **Steps**:
     1. The user selects a task to delete.
     2. The task is removed from the local database and, if online, the deletion is propagated to the server.
     3. The user is notified of the successful deletion.

## Persistence Details
The Task Manager Application utilizes both local and server-side storage for managing tasks. Depending on the device's connectivity, different CRUD operations interact with either or both storage layers.

### Local Database Persistence
- **Create**: New tasks are immediately saved to the local database, ensuring offline access.
- **Update**: Task updates are saved locally, and then synced to the server if the device is online.
- **Delete**: Deleted tasks are removed from the local database, and the changes are reflected on the server once the connection is available.

### Server-Side Persistence
- **Create**: When the device is online, new tasks are automatically pushed to the server for backup and multi-device access.
- **Update**: Any changes made to tasks will be synced with the server, ensuring that updates are reflected across all devices.
- **Delete**: Deleted tasks will be removed from the server when the device is connected to the internet.

## Offline Scenarios

### **Create**
   - **Scenario**: If the user creates a task while offline, the task will be saved to the local database. Once the application detects an internet connection, the task will be automatically synced with the server.
   - **Outcome**: Task creation works smoothly offline, and syncs online later.

### **Read**
   - **Scenario**: The user can view all previously created tasks from the local database even when offline. However, any new updates or tasks created on other devices won't be visible until the application regains internet access.
   - **Outcome**: Reading tasks from the local database is seamless offline.

### **Update**
   - **Scenario**: Users can update tasks while offline. The changes will be saved locally and queued for syncing. Once online, the changes will be pushed to the server.
   - **Outcome**: Offline updates are persisted locally and synced with the server when connected.

### **Delete**
   - **Scenario**: Users can delete tasks offline, and these tasks will be removed from the local database. The application will mark the deletion for server syncing, and once online, the task will also be removed from the server.
   - **Outcome**: Task deletion is fully functional offline, with server updates handled when connectivity is restored.
