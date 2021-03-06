# MovieStore
### Data Centric Development Milestone Project by Owen Cookman

The objective of this webpage is to provide users with a way to search for their favourite movies, movies that they might be interested in or movies that they have been recommended, read the reviews of others or leave a review of their own, they should also be able to delete that review or edit it afterwards.

## UX

The website is aimed at people of any age who have an interest in movies of any genre who would like to read the reviews of others to see if they might like the movie or to leave reviews for others to read.

## Styling choices

#### Colour choices
The webpage has a dark colour pallet, this choice was made so that colours from the different movie posters didn't clash with the page they were rendered on and darkness is often associated with being sat at a cinema screen.

#### Background image
The background image is of an old movie projector, this makes the web page look more interesting on the pages with less content rather than having a solid block of colour. The picture is allowed to resize depending on the size of the page as there may be long lists of movies or reviews rendering on one page, this looks more professional than the image repeating.
An opaquie layover was positioned over the background image to darken down the light areas so that it didn't disrupt the text or draw the eye away from the page content.

#### Font
The font used is Open Sans, this font was chosen to keep the text neutral so not to lean towards fantasy, sci-fi, horror or any other genres, this allows the rendered movie posters to set the feel of the page without any outside influence, the colour for the font is a slightly off white `#fafafa` which was chosen for its neutral colour but also to stand out from the darker background.  

### User Stories

#### User who would like to read reviews to see if they like the sound of a movie
As a user who enjoys watching movies, I would like to search for a movie that I have heard of, read something about it and also read what other people who have already watched it think.

#### User who has watched a movie and would like to give their opinion of that movie
As a user who has recently watched a movie, I would like to leave a review of that movie so that others can make an informed choice as the weather they want to watch it or not.

#### User who would like to know more details about a movie
As a user who enjoys watching movies, I would like to know more details about a particular movie such as who it was directed by.

### Wireframes

Please click [here](wireframes) to view my first draft Wireframes, these were originally made using Balsamiq Mock-ups.

The Registration, Login and Profile were later dropped due to the complexity involved in creating them.
The ability to add, edit and delete reviews was added later to showcase CRUD operations.

## Features

#### Theme
The original **Theme** was taken from the **Bootswatch** themes library, the theme **Journal** was used and then styled with **CSS** to customize it further such as the font used and also the dark background. 

#### Navbar
The **Navbar** used in this project was taken from the **Bootswatch** themes library and edited to fit the needs of the page, it holds a home button in the form of a **FontAwesome** icon and a **Search Bar**.
The Navbar is fully **responsive** and on smaller devices, changes to a burger icon which holds the home button and Search Bar.

#### Search Bar
The **Search Bar** came as part of the **Navbar** taken from **Bootswatch**, when a user inputs a movie name and clicks search or presses enter the input is passed through the `search_result()` function, which is added to the **OMDb API** url along with the **API key** and fired through to the **API**, the response is then iterated through and added to an empty list called `result_list` which is passed to the template **results.html**, this will check if `result_list` is an empty list, if it is it will display a message, if it isn't `result_list` is iterated through in batches of 2 to allow a `<div>` with the class of **row** to be rendered between each result.  

#### Movie Information
When a **result** is selected by the user the **imdbID** value is taken from the variable **imdb_id** which is passed to the `movie()` function, this is then added to a new query url for the **OMDb API** which returns the information about the movie and stores it in the variable **info** which is passed to the template `movie.html` as **movie_info** where select pieces of data are rendered on to the page.

#### Reviews
When a **result** is selected by the user and the movie information is rendered the **Mongo Database** is also queried to search for any **documents** containing the **key** `movieID` with the value of the variable `imdb_id`, this is then iterated through and added to an empty list called `review_list` which is passed to the template `movie.html` which is then passed through a **for loop** to render each review individually.

#### Submitting Reviews
When the **Review** button is selected below the movie information on `movie.html` the `imdbID` from the variable `movie_info` is stored in the variable `imdb_id` and passed as a python variable to the `add_review()` function and renders the template `review.html`. When the **form** is filled in and the **submit** button is selected the `imdbID` is passed to the `submit_review()` function which stores all of the form data in the variable `review` and then passes the variable to the **Mongo Database** to `insert_one` and store the data in its key value pairs.

#### Edit Reviews
When the **Edit** button is pressed underneath the rendered review the value `_id` is taken from the variable review and stored as `review_id` which is passed as a python variable to the `edit_review()` function which passes the id to the** Mongo Database** as a query to `find_one` with the unique id created for the review by the Mongo Database that's **key** is `_id` and renders the template `edit-review.html`. When the **form** that is rendered is filled in and **submitted** the previous review is stored in a variable `old_review` and it's `movieID` is stored in a variable `movie_id`, the form is then requested for the username, comments and score and the `movieID` is set to the variable `movie_id` which is all stored in the variable `new_review`. The Database is then requested to `find_one_and_update` with the variable `old_review` being replace by the variable `new_review`.

#### Delete Reviews
When the **Delete** button is pressed underneath the rendered review the value `_id` is taken from the variable review and stored as `review_id` which is passed as a python variable to the `delete_review()` function which passes the unique id to the **Mongo Database** to `delete_one`. 

### Possible Features To Implement
- A Registration and Login for users would ideally be implemented so that users have a fixed username and are the only ones who can edit or delete their reviews.
- An Amazon affiliate link so that users can choose to buy the movies they like or are interested in watching.
- A confirmation for review deletion to save any miss clicks.

## Technologies Used

- This project uses **HTML**, **CSS** and **Python** programming languages
- [**Visual Studio Code**](https://code.visualstudio.com/) was used as the development IDE
- [**Bootstrap**](https://getbootstrap.com/)
- [**FontAwesome**](https://fontawesome.com/)
- [**Google Fonts**](https://fonts.google.com/)
- [**Popper.js**](https://popper.js.org/)
- this projects wireframes were created on [**Balsamiq**](https://balsamiq.com/)
- The CSS code was validated using the [**W3C Markup Validation Service**](https://validator.w3.org/) website

## Testing

To view the testing carried out on this project please click [here](TESTING.md) for my separate testing file


## Deployment

The Visual Studio Code IDE was used to develop this project and all work was added, committed and pushed to a GitHub repository which was linked with Heroku.

**How to run the project locally**

Note: some of the commands below may differ depending on your chosen IDE and Operating system, the commands below will work with python 3 installed on a Windows operating system.

1. Ensure that you have PIP, Python 3 and Git installed on your machine
2. Create an account on MongoDB Atlas
3. Save a copy of [this](https://github.com/OwenCookman/MovieStore) repository by clicking the "Clone or Download" button at the top of the page and select "Download Zip" to extract the Zip file to your chosen folder
    3. If you have Git installed, use the below command to clone the repository:

    `git clone https://github.com/OwenCookman/MovieStore`

4. Open a terminal session in the unzipped folders directory
5. Create a virtual environment by running the below command

    `python -m .venv venv`

6. Activate the Virtual environment wit the below command

    `.venv/Scripts/acivate`

7. Install required modules by running the below command

    `pip -r requirements.txt`

8. In your local IDE create a file called .flaskenv and inside this file create a "SECRET_KEY" variable and a "MONGO_URI" variable to link to your Mongo Database which should contain a Database called MoviestoreDB with a collection called Reviews.

9. Run the application with the below command

    `python app.py`

10. Visit the website at http://127.0.0.1:5000
    
**How to Deploy the project to Heroku**
Note: You will need an API Key for the [OMDb API](http://www.omdbapi.com/)

1. Create a `requirements.txt` file using the terminal command `pip freeze > requirements.txt`
2. Create a `Procfile` using the terminal command `echo web: python app.py > Procfile`
    2. Please note that if you are using a Windows operating system the `Procfile` may not format properly, please create another file named `Procfile` and copy the contents of the terminal generated `Procfile` over to it, then delete the generated `Procfile`.
3. `git add` and `git commit` both `requirements.txt` and `Procfile` then `git push` your staged files to GitHub
4. Create a new app on [Heroku](https://www.heroku.com) by clicking the "New" button on the Dashboard, give the new app a name and set the region to Europe.
5. From the new applications dashboard click the "Deploy" tab and in the "Deplyoment Method" section select GitHub and confirm that it is connecting to the correct GitHub repository.
6. Select the "Settings" tab and click the Button "Reveal Config Vars" in the Config Vars section and set the below config vars

    | Key | Value |
    |---|---|
    | DEBUG | FALSE |
    | API_KEY | `<your OMDb API Key>` |
    | IP | 0.0.0.0 |
    | PORT | 5000 |
    | SECRET_KEY | `<Your Secret Key Here>` |
    | MONGO_URI | mongodb+srv://`<username>`:`<password>`@cluster0-p9ou4.mongodb.net/Reviews?retryWrites=true&w=majority |

7. Go to the "Deploy" tab and scroll down to the "Manual Deploy" section check that the master branch is selected and click "Deploy Branch"

## Media
The Favicon Icon used in this project was taken from [Icon Finder](https://www.iconfinder.com/icons/3956706/cine_camera_cinema_film_movie_movie_reel_record_video_icon)
The Background image was taken from [Closler](https://closler.org/passion-in-the-medical-profession/from-film-school-to-medical-school-how-john-berger-changed-my-life/attachment/film-reel)

## Acknowledgements

I would like to thank my family and friends for testing this project and reporting back to me with any issues. 
I would also like to thank my mentor Simen Daehlin for his brilliant tutelage As well as the CI Tutor Stephen_CI for his assistance in understanding Python.

This project was created for educational purposes only.
