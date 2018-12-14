# Best practices

## General
* Remove extraneous code (e.g. commented-out CSS rules you're not using, any console.log, commented-out JS that didn't work)
* Units of the project (e.g. files, folders, components, partials, class names, variables), follow a consistent naming convention
* The purpose of the website / application should be clear to the user 

## CSS
* Use your set up snippet (e.g. reset browser default styling, box-sizing: border-box, clearfix, visibilityhidden)
* Wrapper used to constrain content on large displays
* One external .css stylesheet is used for whole project 

## HTML
* Semantic HTML elements are used properly
* Meta viewport tag in the head

## JavaScript
* Use let for variables that will change, const for ones that won't
* Handle your errors (i.e. give the user some feedback if their inputs are incorrect, if they're missing something, or if their search doesn't return anything from the API, etc.)

## React
* Consistent CSS styling pattern is used for whole project
* this.state is never directly changed / .setState() is always used to alter state
* React 'knows' about all DOM changes (e.g. don't use document.getElementById, bind your inputs.)
* No useless constructors
* Unique key value for each child of a .map
* Only import what you use in each file