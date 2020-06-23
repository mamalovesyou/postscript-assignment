# Assignment:

Time: 5h

Please create a tool that can send shipment notifications as text messages. All of the functionality you create must be exposed through a single front-end interface. It must interact with back-end API’s to perform its functions.

The main flows to implement are: 

- A user can choose a particular product and save a draft of a shipping notification for that product. For purposes of this assignment, we want to be able to create different shipping notifications for different products. There can be multiple draft message for a product or one per product, that is up to you.

- A user can also look up draft versions of these text messages that have been saved, and click a button to actually send one of them to a number (which they provide at the time of sending).

Additional details under “User Flows.”

## Tooling (Must use):

Please use the following technologies. If you are unfamiliar with them, learn the minimum required to get the job done. When you send in your assignment, you can tell us which ones you had to learn from scratch and we will take that into account.

- Flask (Python) to create the API endpoints
- Connect to DB using SQLAlchemy or pure SQL
- PostgreSQL database
- ReactJS Front-end (or Flask HTML)
- It is totally fine to use only pure HTML (via Flask) if you are unfamiliar with front-end technologies. There is room on our team for pure backend developers. But if you have front-end skills you can show them here.
- Twilio to send text messages (if for some reason you can’t create a trial account for free credit, let us know)

This does not need to be deployed and available to the internet as long as it can be run locally. The assignment should utilize Docker Compose in order to run locally on any setup.

## User Flows:

- [x] Users should be able to query a list of available product_ids 
- [x] Users should be able to create and save a message for a product
- [x] Saving a message requires a product_id to be attached to the message and should throw an error otherwise
For example, the message object might look like 
```
{ 
  "message" : "Some string",
  "Product_id":1
}
  ```
- [x] Users should be able to view messages for a product
- [x] Users should be able to send messages for a product

- [x] This should utilize the Twilio API -- use a Twilio trial account, it is OK if the message does not send to outside / non-whitelisted numbers.

## Getting Setup:

There are 2 folders contained with this homework:

**`api`**

The `api` folder houses the `Dockerfile` to build and run the `Flask` application against the `db`. It contains a bootstrapped `Flask` object and `Flask-SQLAlchemy` already setup to work with the larger `docker-compose.yml` file of this homework.

**`app`**

The `app` folder will house your frontend code and contains a `Dockerfile` that installs `package.json` with `npm` (or `yarn` if you uncomment it) and then executes `npm start` (or `yarn start`). The package.json does not currently exist (you will have to generate it with any packages you want) and the `docker-compose.yml` will startup the entire application folder when run. Be sure, whatever framework you use, you're able to start the frontend application on port 3000 or you'll need to update the `app/Dockerfile` and `docker-compose.yml` for your frontend port.

__Note:__ If you'd like to use `yarn` instead of `npm`, open the `app/Dockerfile` and swap `npm install --silent` with `yarn install --silent`

### Running the Environment

Once you've created a `package.json` in the `app` folder, you're ready to run the `docker-compose` environment.

By default, when running the `docker-compose` of this repo, the ports will map as follows:

- `api` - Port 5000
- `db` - Port 5432
- `app` - Port 3000

Running the environment is now as easy as `docker compose up`.

- Visit `http://localhost:5000/health-check` to verify the api is working.
- Visit `http://localhost:3000` to see your frontend application

 ### How to use

FIrst step is getting some credentials and a phone number from twilio.

Then create a `.env` file in the same directory as `docker-compose.yml` file.

example:

```
TWILIO_ACCOUNT_SID=<sid>
TWILIO_AUTH_TOKEN=<token>
TWILIO_API_KEY=<api_key>
TWILIO_API_SECRET=<api_secret>
TWILIO_DEFAULT_PHONE_NUM=<phone_number>
```


 Start containers with the classic 
 `docker-compose up`. 
 
 The database will be populated automaticaly after the product table is created (9 products will be inserted).

 Then go to `http://localhost:3000`. You will find a list of product on the left side of the app. Click on one of them. Then you will see the product appear (Title and ID). To add a message you must click on the `Add Message` button which will open a modal with a field. Once the message is added, the modal close itself and the product is updated with this new message in the list. To send a message, you must click on the `Send` button bellow the message you want to send. A modal will prompt and you must enter a phone number. Click on send and when the message is send the modal disapears. 

