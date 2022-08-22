# Todo-List-Database

## Table of contents

- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
- [Author](#author)

## My process

### Built with

- HTML5
- CSS3
- Bootstrap
- MongoDB
- Mongoose
- EJS
- Lodash
- Node.js
- Express.js
- Heroku

### What I learned

This ToDo List project was very useful in learning how to manipulate elements of a database on a webpage and the different ways you are able to display them and even remove them when necessary. Using EJS also allowed me to make the webpage dynamic in displaying the different items that the user decides to add or remove from their lists.
Code written in this project that I want to highlight:

```Node.js
  if (listName === "Today"){
    item.save();
    res.redirect("/");
  } else {
    List.findOne({name: listName}, (err, foundList) => {
      foundList.items.push(item);
      foundList.save();
      res.redirect("/" + listName);
    });
  }
});
```
Here the code displayed allows the user to see all of the saved ToDo list items they have created clearly displayed for them on the webpage, with a new item being added dynamically every time they press the plus (+) button.

```Node.js
app.post("/delete", (req,res) => {
  const checkedItemId = req.body.checkbox;
  const listName = req.body.listName;

  if (listName === "Today") {
    Item.findByIdAndRemove(checkedItemId, (err) => {
      if (!err) {
        console.log("Successfully deleted checked item.");
        res.redirect("/");
      }
    });
  } else {
    List.findOneAndUpdate({name: listName}, {$pull: {items: {_id: checkedItemId}}}, (err, foundList) => {
      if (!err) {
        res.redirect("/" + listName);
      }
    });
  }
});
```
The user is able to delete finsihed ToDo list items by checking them with a check box. Once checked, the item is then deleted from the ToDo list as well as the database.

### Continued development

This project was quite complex for how seemingly simple the end result is. One thing that users may not know is that they also have the ability to create separate ToDo lists by typing the name of that ToDo list into the browser. For example, if they were to put “/Shopping” at the end of the URL, it would open up another ToDo list with that title. The user would then be able to switch back and forth between any created ToDo lists and the original ToDo list by simply typing it into the URL. For continued development, I would love to create a button with the ability to create separate ToDo Lists directly from the webpage, and a dropdown menu so that the user is able to easily navigate between the lists.

## Author

- Website - [Elyse Chambers](https://www.diaryofelyse.com)
- Frontend Mentor - [Elyseeloo](https://www.frontendmentor.io/profile/Elyseeloo)
- Twitter - [@Elyseeloo\_](https://www.twitter.com/elyseeloo_)
