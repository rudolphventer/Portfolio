

# 🌊 Welcome to my portfolio! 🌊

My name is Rudolph Venter and this is my portfolio. 
There are many like it, but this one is mine.

## --🧱--The Stack--🧱--

The site is built using Vue.js, Node.js with the vue-cli is used to create the project.
The site is compiled to static files and then hosted on an Amazon S3 bucket, this all happens automatically. **I did not use bootstrap.** *Not even a little bit.*

I did include some NPM modules though:
* [Chart.js](https://www.chartjs.org/)
* [vue-css-donut-chart](https://www.npmjs.com/package/vue-css-donut-chart)
* [moment.js](https://www.npmjs.com/package/moment)
* [Axios](https://www.npmjs.com/package/axios)

I also used the amazing [LinearIcons](https://linearicons.com/) Icon pack as well as an AWS S3 bucket and AWS CodePipeline and Github for CI/CD for easy updating in the future as well as dynamic Vue single file components. (because my portfolio site definitely needs to be scalable to the same degree as Twitter)

Lastly, the logo at the top is my own, if you see it somewhere then chances are I put it there.

## --⚙--How it Works--⚙--
Every time I commit to the master branch, a webhook tells AWS CopePipeline to copy the source files from Github and build the site to static files using the instructions in the _buildfile.yml_ file. This is then built and the files are uploaded to my S3 bucket. Since all the files are static, this means that all the API calls happen client side and I don't have to rent a CPU from Jeff Bezos.

## --🌟--What's it do Though?--🌟--
Good question! I used a custom CSS grid card layout, each card is it's own component and does something different. 

In order: (or not, depending on your screen size, its reactive!)

- A bio card with data from Github's API
- A static "about me" card, written in good old HTML
- Roughly 3 cards that show off my favorite public repos with data from Github's API, the language breakdown is a pure CSS doughnut chart from [here](https://www.npmjs.com/package/vue-css-donut-chart) (I didn't reinvent the wheel, or doughnut, in this case)
- The bar charts uses [Chart.js](https://www.chartjs.org/) and static data to give a rough impression of how good I think I am at some specific things
- Events are an odd thing to include on a portfolio, but these events come straight from my own event booking platform [Conductor](https://conductor-booker.herokuapp.com/), I pull recent event data from the REST API and display theme here
- My take on the "Contact Me" section, this card verifies your email and then uses the awesome Telegram Bot API to transport your message from your screen to mine via a Telegram bot 🤖
- The qualifications and projects cards show more static data about my qualifications and projects
- The line graph is also a [Chart.js](https://www.chartjs.org/)  chart but this one uses actual data from the Github API to show my commits to **public** repos over the last 90 days, it doesn't look like much but all my good stuff is top secret so I can't brag about it
- The background scrolls. You are welcome.


## --💻--Project setup--💻--
In case you want to see this page running for yourself to confirm it's not just a *very* high quality GIF, clone it and follow these steps.

### Install all the dependencies
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
