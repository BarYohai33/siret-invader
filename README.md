# Siret Invader

`Siret Invader` is a tool to index big CSV file into MongoDB while parallelizing processes for best performance.

## Installation and Usage

Prerequisites: [Node.js](https://nodejs.org/en/) (>=8.x), yarn or npm.

```
$ npm install
or
$ yarn
```

You must first run `node entry.js` (or `yarn app`), then you can enter the manager by `node siretManager.js` (or `yarn pm`).

**Note**: Before processing files, don't forget to split the big one (`4th action` in the `Siret Manager`).

You can use the `Siret Manager` to do every action on the app, just by entering a number corresponding to the action.

* 1 - Start the files processing.
* 2 - Pause all the processes.
* 3 - Resume all the processes.
* 4 - Split the big file into smaller, processable pieces.

**Note**: Simply press (Ctrl/Cmd)+C to quit the `Siret Manager`.

## Third-Party Used 

* [pm2](https://github.com/Unitech/pm2) for process management.
* [chalk](https://github.com/chalk/chalk) for beautiful colored log in the console.
* [figlet](https://github.com/patorjk/figlet-cli) for stylish ASCII text in the console.
* [mongodb](https://github.com/mongodb/mongo) for the great NoSQL storage.
* [split](https://github.com/dominictarr/split) for streaming a file line by line.
* [ESlint](https://github.com/eslint/eslint) and [AirBnB style guide](https://github.com/airbnb/javascript) for linting.

## Configuration

You can configure the app as you wish by populating the **first element** of the **apps array** in the `process.json` file.

For instance, you may want to use the maximum number of cores of your computer for the processing, simply put 
```json
{
    ...,
    "instances": "max"
}
```

The `cropSize` property is equivalent to the amount of lines of the file processed given to MongoDB for insertion.
* For better performance but more memory usage, use higher value (10000 is a good exemple)
* For lower memory usage but less performance, use lower value (1000 is a good exemple)

## What to Know

The application is developed in a simple architecture arranged into two big parts :
  * The `entry.js`, the main file which consists of inter-communication between processes.
  * The `app.js` which consists of the main role of the app : processing files (pausing and resuming the processing also), that can be only ran via `entry.js` (no `node app.js` allowed).

**Note**: The operation of **spliting the csv into smaller pieces** doesn't need the main file to be running, you can simply call the `splitCsv` function from `utils.js` (the same action in `Siret Manager` does need it though)
  
The `siretManager.js` file is a little CLI helping us to do different actions to manage our app.

The `processAction.js` file are only helpers for `sending file`, `pausing` and `resuming` process with the help of `PM2 API`.

The `processLinker.js` file is only there to be the bridge for communicating between the `Siret Manager` and the PM2 processes.

The `utils.js` file consists in a number of small functions which are pretty straigthforward to understand.

---

Thanks for using this project `;)`