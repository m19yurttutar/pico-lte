# MongoDB Atlas Data API Usage

Welcome to our user guide on harnessing the dynamic duo of Pico LTE and MongoDB Atlas Data API! This guide will walk you through the process of utilizing the Pico LTE to seamlessly interact with MongoDB Atlas via its Data API. By the end of this guide, you'll have a comprehensive grasp of how to discover, add, modify, and remove data from your MongoDB database.

Before diving into the tutorial, it's imperative to ensure that you've completed the installation and configuration steps for the Pico LTE SDK. Please take a moment to review the system requirements outlined below. If you haven't yet completed the SDK installation, we recommend referring to the relevant page for detailed instructions. Please note that the specifics of these installation steps won't be covered in this guide. Let's get started on our journey to harnessing the power of Pico LTE and MongoDB Atlas Data API!

## System Requirements

| Hardware Requirements                                     | Software Requirements        |
| :-------------------------------------------------------- | :--------------------------- |
| <ul><li>Sixfab Pico LTE</li><li>Micro USB Cable</li></ul> | <ul><li>Thonny IDE</li></ul> |

If you have completed all the requirements, you are ready to use MongoDB Atlas Data API with the Pico LTE device.

Let's get started!

## Preparing Coding Environment

1. Download the [Pico LTE SDK repository](https://github.com/sixfab/picocell_python-sdk) to your local machine. If you have already downloaded it, skip this step.

2. Open script **"examples → mongodb_atlas → find_one.py / find_many.py / insert_one.py / insert_many.py / update_one.py / update_many.py / delete_one.py / delete_many.py"** from the repository via Thonny IDE.

3. If you haven't, create a `config.json` file in the root directory of Pico LTE device.

## MongoDB Atlas Data API

1. Login to MongoDB Atlas Database

   If you have a MongoDB Atlas account, sign in from [this page](https://account.mongodb.com/account/login), otherwise create a MongoDB Atlas account from the [register page](https://www.mongodb.com/cloud/atlas/register).

2. Create a New Organization

   Create your organization by naming it. You can also configure optional fields according to your needs.

   > **Note:** The organization creation process may be automatic for those who register for the first time. In this case, create a new organization or continue the guide from the next stage.

   ![Create an Organization](/assets/1.png)
   ![Name Your Organization](/assets/2.png)
   ![Create Organization](/assets/3.png)

3. Create a New Project

   Create your project, in which you will deploy your database with various configurations.

   > **Note:** The project creation process may be automatic for those who register for the first time. In this case, create a new project or continue the guide from the next stage.

   ![New Project](/assets/4.png)
   ![Name Your Project](/assets/5.png)
   ![Create Project](/assets/6.png)

4. Create a Deployment

   Deploy your database by configuring various settings.

   ![Create a Deployment](/assets/7.png)

   - Choose the plan you want according to your project. If you will use the application to examine it, you can use the M0 (shared) plan, which offers one free cluster service for each project.

   - Name your cluster and tick the checkboxes below. Sample dataset is important for using examples in PicoLTE MicroPython SDK.

   - Change settings such as provider and region according to your preference. These settings may affect the response speed you will receive in the project.

   - Click Create Deployment button for creating your deployment.

   > **Note:** After clicking the "Create deployment" button, you can proceed to the next stage by closing the **"Connect to [CLUSTER_NAME]"** page. This process is not required since performs authorization with API KEY in the application.

   ![Name Your Project](/assets/8.png)

5. Enable Data API

   Enable the Data API that will act as a bridge between the application and the database.

   - Select your project whose API you will activate and activate your Data API by making the following configurations according to your preference.

   ![Name Your Project](/assets/9.png)

   - Create your API key and copy it into your `config.json` file.

   ![Create API Key](/assets/10.png)

   ![Copy API Key](/assets/11.png)

   - Then, copy the URL Endpoint(Base URL) on the Data API page to the `config.json` file. Additionally, to perform read and write operations on your database, set the access setting in your cluster's Data API Access section.

   ![Copy URL Endpoint](/assets/12.png)

Now your Pico LTE is ready to interact seamlessly with the MongoDB Atlas Data API. Let's give a few examples of how to interact with MongoDB Atlas Data API using our PicoLTE device

## Examples

### 1. Find One Document

This example shows how to find a document from MongoDB Atlas with an HTTP POST request.

- Open Thonny and create the config.json file as shown below. Use the information you copied earlier.

  ```json
  {
    "mongodb_atlas": {
      "base_url": "[BASE_URL]",
      "api_key": "[API_KEY]"
    }
  }
  ```

- Run the file **"find_one.py"** located in the **"examples → mongodb-atlas"** file directory. The dictionary type variable, "payload" should be changed according to your database data. In the pictures below, the part that says "PicoLTE" shows `CLUSTER_NAME`, "sample_mflix" shows `DATABASE_NAME`, and "comments" shows `COLLECTION_NAME`. An object consisting of [Query Operators](https://www.mongodb.com/docs/atlas/app-services/mongodb/crud-and-aggregation-apis/#query-operators) that will filter the desired document must be entered into the `filter`. For details check [find one document](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi/#operation/findOne).

  ```python
  payload = {
   "dataSource": "[CLUSTER_NAME]",
   "database": "[DATABASE_NAME]",
   "collection": "[COLLECTION_NAME]",
   "filter": "[QUERY_OPERATORS]",
  }
  ```

  ![Browse Collections](/assets/13.png)
  ![Get Database Value](/assets/14.png)

### 2. Find Documents

This example shows how to find documents from MongoDB Atlas with an HTTP POST request.

- Open Thonny and create the config.json file as shown below. Use the information you copied earlier.

  ```json
  {
    "mongodb_atlas": {
      "base_url": "[BASE_URL]",
      "api_key": "[API_KEY]"
    }
  }
  ```

- Run the file **"find_many.py"** located in the **"examples → mongodb-atlas"** file directory. The dictionary type variable, "payload" should be changed according to your database data. In the pictures below, the part that says "PicoLTE" shows `CLUSTER_NAME`, "sample_mflix" shows `DATABASE_NAME`, and "comments" shows `COLLECTION_NAME`. An object consisting of [Query Operators](https://www.mongodb.com/docs/atlas/app-services/mongodb/crud-and-aggregation-apis/#query-operators) that will filter the desired document must be entered into the `filter`. For details check [find documents](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi/#operation/find).

  ```python
  payload = {
   "dataSource": "[CLUSTER_NAME]",
   "database": "[DATABASE_NAME]",
   "collection": "[COLLECTION_NAME]",
   "filter": "[QUERY_OPERATORS]",
  }
  ```

  ![Browse Collections](/assets/13.png)
  ![Get Database Value](/assets/14.png)

### 3. Insert One Document

This example shows how to insert a document from MongoDB Atlas with an HTTP POST request.

- Open Thonny and create the config.json file as shown below. Use the information you copied earlier.

  ```json
  {
    "mongodb_atlas": {
      "base_url": "[BASE_URL]",
      "api_key": "[API_KEY]"
    }
  }
  ```

- Run the file **"insert_one.py"** located in the **"examples → mongodb-atlas"** file directory. The dictionary type variable, "payload" should be changed according to your database data. In the pictures below, the part that says "PicoLTE" shows `CLUSTER_NAME`, "sample_mflix" shows `DATABASE_NAME`, and "comments" shows `COLLECTION_NAME`. A document of type object to insert into the collection must be entered into the `document`. For details check [insert one document](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi/#operation/insertOne).

  ```python
  payload = {
   "dataSource": "[CLUSTER_NAME]",
   "database": "[DATABASE_NAME]",
   "collection": "[COLLECTION_NAME]",
   "document": "[DOCUMENT_TO_INSERT]",
  }
  ```

  ![Browse Collections](/assets/13.png)
  ![Get Database Value](/assets/14.png)

### 4. Insert Documents

This example shows how to insert documents from MongoDB Atlas with an HTTP POST request.

- Open Thonny and create the config.json file as shown below. Use the information you copied earlier.

  ```json
  {
    "mongodb_atlas": {
      "base_url": "[BASE_URL]",
      "api_key": "[API_KEY]"
    }
  }
  ```

- Run the file **"insert_many.py"** located in the **"examples → mongodb-atlas"** file directory. The dictionary type variable, "payload" should be changed according to your database data. In the pictures below, the part that says "PicoLTE" shows `CLUSTER_NAME`, "sample_mflix" shows `DATABASE_NAME`, and "comments" shows `COLLECTION_NAME`. The documents of type array of object to insert into the collection must be entered into the `documents`. For details check [insert documents](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi/#operation/insertMany).

  ```python
  payload = {
   "dataSource": "[CLUSTER_NAME]",
   "database": "[DATABASE_NAME]",
   "collection": "[COLLECTION_NAME]",
   "documents": "[DOCUMENTS_TO_INSERT]",
  }
  ```

  ![Browse Collections](/assets/13.png)
  ![Get Database Value](/assets/14.png)

### 5. Update One Document

This example shows how to update a document from MongoDB Atlas with an HTTP POST request.

- Open Thonny and create the config.json file as shown below. Use the information you copied earlier.

  ```json
  {
    "mongodb_atlas": {
      "base_url": "[BASE_URL]",
      "api_key": "[API_KEY]"
    }
  }
  ```

- Run the file **"update_one.py"** located in the **"examples → mongodb-atlas"** file directory. The dictionary type variable, "payload" should be changed according to your database data. In the pictures below, the part that says "PicoLTE" shows `CLUSTER_NAME`, "sample_mflix" shows `DATABASE_NAME`, and "comments" shows `COLLECTION_NAME`. An object consisting of [Query Operators](https://www.mongodb.com/docs/atlas/app-services/mongodb/crud-and-aggregation-apis/#query-operators) that will filter the desired document must be entered into the `filter`. An object consisting of [Update Operators](https://www.mongodb.com/docs/atlas/app-services/mongodb/crud-and-aggregation-apis/#update-operators), the new version of the values of the filtered document that want to change, must be entered into the `update`. For details check [update one document](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi/#operation/updateOne).

  ```python
  payload = {
   "dataSource": "[CLUSTER_NAME]",
   "database": "[DATABASE_NAME]",
   "collection": "[COLLECTION_NAME]",
   "filter": "[QUERY_OPERATORS]",
   "update": "[UPDATE_OPERATORS]"
  }
  ```

  ![Browse Collections](/assets/13.png)
  ![Get Database Value](/assets/14.png)

### 6. Update Documents

This example shows how to update documents from MongoDB Atlas with an HTTP POST request.

- Open Thonny and create the config.json file as shown below. Use the information you copied earlier.

  ```json
  {
    "mongodb_atlas": {
      "base_url": "[BASE_URL]",
      "api_key": "[API_KEY]"
    }
  }
  ```

- Run the file **"update_many.py"** located in the **"examples → mongodb-atlas"** file directory. The dictionary type variable, "payload" should be changed according to your database data. In the pictures below, the part that says "PicoLTE" shows `CLUSTER_NAME`, "sample_mflix" shows `DATABASE_NAME`, and "comments" shows `COLLECTION_NAME`. An object consisting of [Query Operators](https://www.mongodb.com/docs/atlas/app-services/mongodb/crud-and-aggregation-apis/#query-operators) that will filter the desired document must be entered into the `filter`. An object consisting of [Update Operators](https://www.mongodb.com/docs/atlas/app-services/mongodb/crud-and-aggregation-apis/#update-operators), the new version of the values of the filtered document that want to change, must be entered into the `update`. For details check [update documents](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi/#operation/updateMany).

  ```python
  payload = {
   "dataSource": "[CLUSTER_NAME]",
   "database": "[DATABASE_NAME]",
   "collection": "[COLLECTION_NAME]",
   "filter": "[QUERY_OPERATORS]",
   "update": "[UPDATE_OPERATORS]"
  }
  ```

  ![Browse Collections](/assets/13.png)
  ![Get Database Value](/assets/14.png)

### 7. Delete One Document

This example shows how to delete a document from MongoDB Atlas with an HTTP POST request.

- Open Thonny and create the config.json file as shown below. Use the information you copied earlier.

  ```json
  {
    "mongodb_atlas": {
      "base_url": "[BASE_URL]",
      "api_key": "[API_KEY]"
    }
  }
  ```

- Run the file **"delete_one.py"** located in the **"examples → mongodb-atlas"** file directory. The dictionary type variable, "payload" should be changed according to your database data. In the pictures below, the part that says "PicoLTE" shows `CLUSTER_NAME`, "sample_mflix" shows `DATABASE_NAME`, and "comments" shows `COLLECTION_NAME`. An object consisting of [Query Operators](https://www.mongodb.com/docs/atlas/app-services/mongodb/crud-and-aggregation-apis/#query-operators) that will filter the desired document must be entered into the `filter`. For details check [delete one document](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi/#operation/deleteOne).

  ```python
  payload = {
   "dataSource": "[CLUSTER_NAME]",
   "database": "[DATABASE_NAME]",
   "collection": "[COLLECTION_NAME]",
   "filter": "[QUERY_OPERATORS]"
  }
  ```

  ![Browse Collections](/assets/13.png)
  ![Get Database Value](/assets/14.png)

### 8. Delete Documents

This example shows how to delete documents from MongoDB Atlas with an HTTP POST request.

- Open Thonny and create the config.json file as shown below. Use the information you copied earlier.

  ```json
  {
    "mongodb_atlas": {
      "base_url": "[BASE_URL]",
      "api_key": "[API_KEY]"
    }
  }
  ```

- Run the file **"delete_many.py"** located in the **"examples → mongodb-atlas"** file directory. The dictionary type variable, "payload" should be changed according to your database data. In the pictures below, the part that says "PicoLTE" shows `CLUSTER_NAME`, "sample_mflix" shows `DATABASE_NAME`, and "comments" shows `COLLECTION_NAME`. An object consisting of [Query Operators](https://www.mongodb.com/docs/atlas/app-services/mongodb/crud-and-aggregation-apis/#query-operators) that will filter the desired document must be entered into the `filter`. For details check [delete documents](https://www.mongodb.com/docs/atlas/app-services/data-api/openapi/#operation/deleteMany).

  ```python
  payload = {
   "dataSource": "[CLUSTER_NAME]",
   "database": "[DATABASE_NAME]",
   "collection": "[COLLECTION_NAME]",
   "filter": "[QUERY_OPERATORS]"
  }
  ```

  ![Browse Collections](/assets/13.png)
  ![Get Database Value](/assets/14.png)
