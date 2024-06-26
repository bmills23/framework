# Bryan's Blog Framework

THIS IS MOSTLY A PET PROJECT AND IS NOT INTENDED FOR COMMERCIAL USE OR WHERE SENSITIVE DATA IS USED.  This is obviously still a work in progress, and I will condense the process at some point.  

This blog framework is designed to give a set structure to a beginner blog.

This framework assumes the use of an internet-based MySQL database (see /routes/database.js) such as Planetscale DB.

This blog structure was setup with remote file storage using AWS.

## Step 1:

Set up a remote MySQL database.  I used Planetscale DB. Setup like this.

Copy and paste the scripts into your database console.

`CREATE TABLE user (
    id INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    fName VARCHAR(45) NOT NULL,
    lname VARCHAR(45) NOT NULL,
    email VARCHAR(45) NOT NULL,
    password VARCHAR(255) NOT NULL,
    website VARCHAR(255) NOT NULL,
    social json NOT NULL,
    navColor VARCHAR(7) NOT NULL DEFAULT '#FFFFFF'
);`

`CREATE TABLE post (
    id INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    content LONGTEXT NOT NULL,
    trueContent LONGTEXT NOT NULL,
    uploadedAt BIGINT NOT NULL,
    updatedDate BIGINT NOT NULL,
    title TEXT NOT NULL,
    fileAmount TINYINT NOT NULL,
    featured TINYINT(1) NOT NULL,
    userID INT NOT NULL   
);`

`CREATE TABLE aboutme (
    content LONGTEXT NOT NULL,
    trueContent LONGTEXT NOT NULL,
    uploadedAt BIGINT NOT NULL PRIMARY KEY,
    updatedDate BIGINT NOT NULL,
    fileAmount INT NOT NULL DEFAULT 0,
    aboutMeFiles INT NOT NULL DEFAULT 0,
    bannerContent LONGTEXT NOT NULL,
    userID INT NOT NULL,
    aboutMeColor VARCHAR(7) NOT NULL
);`

`CREATE TABLE aboutMeImages (
    ID INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    x INT NOT NULL,
    y INT NOT NULL,
    src VARCHAR(1000) NOT NULL,
    uploadedAt BIGINT NOT NULL,
    imageType VARCHAR(100) NOT NULL,
    userID INT NOT NULL
);`

`CREATE TABLE blogImages (
    ID INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    x INT NOT NULL,
    y INT NOT NULL,
    src VARCHAR(1000) NOT NULL,
    uploadedAt BIGINT NOT NULL,
    imageType VARCHAR(100) NOT NULL,
    userID INT NOT NULL
);`

`CREATE TABLE gallery (
    ID INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    uploadedAt BIGINT NOT NULL,
    name VARCHAR(1000) NOT NULL,
    caption VARCHAR(100) NOT NULL,
    userID INT NOT NULL
);`

## Step 2: 

Set up a .env file in the root directory with variables SESSION_SECRET, DB_URL, PORT, REGION, ACCESS_KEY, SECRET_ACCESS_KEY, USER_REGION, IDENTITY_POOL_ID, BUCKET, and ID.

SESSION_SECRET will be a key that is used for encrypting cookies.  I used a long string of digits and letters such as AS7D98FTA0SDGBFANKSDGVA8SDHGGFAIOPSJDFASBD80FHASDFNKAS 

DB_URL will be the URL given by your respective db service.

PORT will be used for the app.listen() function at the end of index.js in the root directory.  This will be provided by whatever service you use.  For instance, I use fly.io which defaults to '0.0.0.0:8080' 

The next six variables are keys from your AWS bucket.

ID = the autoincrementing ID from the user database. We will create a user in the next step.

Obviously, removing the .env file will be a priority so this process can be reduced down so no programming experience is required.  

## Step 3: 

Expose register.js and register.ejs in the Unused Folder.  Drag register.js to routes and register.ejs to views folder and then redeploy the website. In your website, navigate to yourwebsitehere.com/register.  Fill out the form and submit.  You now have a partially complete user entry in your database.  Linkedin, facebook, instagram and twitter icons are implementable, but social media functionality is not implemented in the register form.  You will have to update the json in the user field manually if you want your social media to appear in the footer (navigate to the footer element in /views/partials/footer.ejs to see what I'm talking about). 

Example of how to do that in your respective DB: 

`INSERT INTO user (social) VALUES (
    '{
        "facebook": "https://www.facebook.com/yourpage",
        "linkedin": "https://www.linkedin.com/in/yourprofile",
        "instagram": "https://www.instagram.com/youraccount",
        "twitter": "https://twitter.com/yourhandle"
    }'
); WHERE id = 1;`

