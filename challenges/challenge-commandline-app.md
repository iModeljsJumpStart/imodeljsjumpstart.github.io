# Challenge: Create a CommandLine App

## Summary

By completing this you will learn how to:
- Create a small command line app
- Use supplied code to query an [iModel Snapshot](https://www.imodeljs.org/learning/backend/accessingimodels/)

## Setup

1. Install the [required tools](https://www.imodeljs.org/getting-started/)

2. That's it!

## Goals

**Goal** Follow the instructions to create your own skeleton command line app with queries an iModel Snapshot and outputs a list of categories.

**Bonus goal** Modify the app to query for views instead.

## Solution

The best way to learn is by doing!  But, if you want to skip ahead you can go right to the [full solution](https://github.com/iModeljsJumpStart/challenge-commandline-app-solution).

## Instructions

1. The full instructions are here: [Writing Command Line Applications with iModel.js](https://medium.com/imodeljs/writing-command-line-applications-with-imodel-js-ba06f4531cc2).  All you need to do is follow along with the blog post.  You will create a few files, cut-and-paste some code, then install, build, and run your own command line app.

## Instructions for bonus goal

1. See if you can modify the app so that it prints out a list of views, instead of a list of categories.  Easy peasy!

    If you need help try <a onclick="toggleHint('hints-1')">these hints</a>.
<div class="hint-group" id="hints-1" style="display:none">

<a onclick="toggleHint('hint-1-1')">Hint 1</a>
<div class="hint" id="hint-1-1" style="display:none">
The base class for view definition elements is <code>ViewDefinition</code>.
</div>
<br>

<a onclick="toggleHint('hint-1-2')">Hint 2</a>
<div class="hint" id="hint-1-2" style="display:none">
Use this query: <code>SELECT ECInstanceId FROM bis.ViewDefinition</code>
</div>
<br>

<a onclick="toggleHint('hint-1-3')">Hint 3</a>
<div class="hint" id="hint-1-3" style="display:none">
Find the call to iModel.withPreparedStatement and replace <code>bis.Category</code> with the <code>bis.ViewDefinition</code></a>
</div>
<br>
</div>

2. Try some experiments.  What data is interesting to you?

## Conclusion

So, were you up to the challenge? Check out how we solved it by viewing our [full solution](https://github.com/iModeljsJumpStart/challenge-color-by-category-solution/blob/master/src/frontend/app/ColorByCategory.ts).  Let us know if you have a better way.

Feedback is welcome!  Let us know via the [iModel.js community](https://www.imodeljs.org/learning/communityresources/).


<script type="text/javascript">
    function toggleHint (hintId) {
        var hint = document.getElementById(hintId);
        if (hint.style.display === "none") {
        hint.style.display = "block";
        } else {
        hint.style.display = "none";
        }
    }
</script>

