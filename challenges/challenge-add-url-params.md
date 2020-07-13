# Challenge: Add URL Parameters

## Summary

By completing this challenge you will learn how to:
- Open iModels by passing iModel/Project names in the URL.
- Use URL params to generate shareable links that can emphasize and zoom into elements.

## Setup

1. Install the [required tools](https://www.imodeljs.org/getting-started/)

2. Clone the repo [from github](https://github.com/iModeljsJumpStart/challenge-add-url-params)

3. `npm install`

4. `npm run build`

5. `npm run start`

6. Head over to the [registration dashboard](https://www.imodeljs.org/getting-started/registration-dashboard/?tab=1) to create some sample iModels.

The app won't be able to open any iModels as is. You will need to add the functionality to pass iModel and Project name in the URL and then open the iModel.

NOTE: The project name is the same as iModel name for iModels created using [registration dashboard](https://www.imodeljs.org/getting-started/registration-dashboard/?tab=1).

## Goals

**Goal** Follow the instructions to create your own iModel.js web app that can open an iModel by passing in iModel and Project name in URL.

**Bonus** Modify the app to emphasize and zoom into elements by passing list of element IDs in URL.

**Double Bonus** Deploy the app by completing the Deploy iModel.js App [challenge](./challenge-deploy-imodeljs-app.md) and generate a shareable link that highlights specific elements.

## Solution

The best way to learn is by doing! But, if you want to skip ahead you can go right to the [full solution](https://github.com/iModeljsJumpStart/challenge-add-url-params-solution).

## Instructions

1. The full instructions are here: [Super URLs](https://medium.com/imodeljs/super-urls-a6eb6b275a9).  All you need to do is follow along with the blog post.  You will modify the app to add ability to take in URL params. These will then be used open a specific project/iModel.

## Instructions for Bonus

1. See if you can modify the URL to take in a list of element IDs. Then use these IDs to emphasize and zoom into the elements.

    If you need help try <a onclick="toggleHint('hints-1')">these hints</a>.
<div class="hint-group" id="hints-1" style="display:none">

<a onclick="toggleHint('hint-1-1')">Hint 1</a>
<div class="hint" id="hint-1-1" style="display:none">
You can view element IDs by opening the Chrome console (Ctrl+Shift+J) and clicking on an element.
</div>
<br>

<a onclick="toggleHint('hint-1-2')">Hint 2</a>
<div class="hint" id="hint-1-2" style="display:none">
Element IDs can be separated in URL by adding spaces between them. Parse the spaces later to create list of IDs.
</div>
<br>

<a onclick="toggleHint('hint-1-3')">Hint 3</a>
<div class="hint" id="hint-1-3" style="display:none">
API for <a href="https://www.imodeljs.org/reference/imodeljs-frontend/rendering/emphasizeelements/emphasizeelements/" target="_blank">emphasizing elements.</a>
</div>
<br>

<a onclick="toggleHint('hint-1-4')">Hint 4</a>
<div class="hint" id="hint-1-4" style="display:none">
API for <a href="https://www.imodeljs.org/reference/imodeljs-frontend/views/viewport/zoomtoelements/" target="_blank">zooming into elements.</a>
</div>
<br>

</div>

2. If you [deploy the app](./challenge-deploy-imodeljs-app.md): use your new feature to generate shareable links that highlight specific element(s).
Maybe you can find something more interesting than the dairy cooler ;)

NOTE: If you share links with a colleague/friend, they will need a CONNECT [account](https://ims.bentley.com/IMS/Account/Login) to view the iModel. Don't forget to add them to the project using the [registration dashboard](https://www.imodeljs.org/getting-started/registration-dashboard/?tab=1)!

## Conclusion

So, were you up to the challenge? Check out how we solved it by viewing our [full solution](https://github.com/iModeljsJumpStart/challenge-add-url-params-solution/blob/master/src/frontend/components/App.tsx).  Let us know if you have a better way.

Feedback is welcome! Let us know via the [iModel.js community](https://www.imodeljs.org/learning/communityresources/).

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
