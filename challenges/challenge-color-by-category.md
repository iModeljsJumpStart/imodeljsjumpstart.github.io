# Challenge: Override Color by Category

## Summary

By completing this you will learn how to:
- Clone, install, and run a basic desktop viewer app.
- Modify the application with custom behavior.
- Write code that overrides the color of elements in the view.
- For the bonus, write your own ECSQL query
- For the bonus, send a message to the user

## Setup

1. Install the [required tools](https://www.imodeljs.org/getting-started/)

2. Clone the repo [from github](https://github.com/iModeljsJumpStart/challenge-color-by-category)

3. `npm install`

4. `npm run`

5. `npm run`

6. The app should run and display a small model of a plant.

Note: The app will be built automatically in step 3, and will be automatically updated anytime you make code changes.  There is no need to stop and restart
the app manually when making code changes.

## Goals

**Goal** Add code to the skeleton app such that whenever the user selects an element, the app will override the color of that element and also every element that shares the same category as that element.

**Bonus goal** is to further extend the app so that a message is displayed to the user telling him the name of the category of the selected element.

## Solution

The best way to learn is by doing!  But, if you want to skip ahead you can go right to the [full solution](https://github.com/iModeljsJumpStart/challenge-color-by-category-solution/blob/master/src/frontend/app/ColorByCategory.ts).

## Instructions

1. Find the method [ColorByCategoryListener.overrideElementColors](https://github.com/iModeljsJumpStart/challenge-color-by-category/blob/46b662475827c3f25ddfcfafddcc11ad36b661bb/src/frontend/app/ColorByCategory.ts#L43).

2. Implement the method.  Use the Emphasize Elements [sample](https://www.imodeljs.org/sample-showcase/?group=Viewer+Features&sample=emphasize-elements-sample) as a starting point.

    If you need help try <a onclick="toggleHint('hints-1')">these hints</a>.
<div class="hint-group" id="hints-1" style="display:none">

<a onclick="toggleHint('hint-1-1')">Hint 1</a>
<div class="hint" id="hint-1-1" style="display:none">
The method you need to call is <a href="https://www.imodeljs.org/reference/imodeljs-frontend/rendering/emphasizeelements/overrideelements" target="_blank">EmphasizeElements.overrideElements</a>
</div>
<br>

<a onclick="toggleHint('hint-1-2')">Hint 2</a>
<div class="hint" id="hint-1-2" style="display:none">
You need a <a href="https://www.imodeljs.org/reference/ui-components/viewport" target="_blank">Viewport</a>. You can use static methods on <a href="https://www.imodeljs.org/learning/frontend/imodelapp">IModelApp</a> to get the viewport with which the user is currently interacting.
</div>
<br>

<a onclick="toggleHint('hint-1-3')">Hint 3</a>
<div class="hint" id="hint-1-3" style="display:none">
The viewport you need is <code>IModelApp.viewManager.selectedView</code>
</div>
<br>

<a onclick="toggleHint('hint-1-4')">Hint 4</a>
<div class="hint" id="hint-1-4" style="display:none">
To get the color value, you need to call <a href="https://github.com/iModeljsJumpStart/challenge-color-by-category/blob/46b662475827c3f25ddfcfafddcc11ad36b661bb/src/frontend/app/ColorByCategory.ts#L32" target="_blank">ColorByCategoryListener.getNextColor</a>
</div>
<br>

<a onclick="toggleHint('hint-1-5')">Hint 5</a>
<div class="hint" id="hint-1-5" style="display:none">
<code><pre>
private overrideElementColors(ids: Id64String[]) {
const vp = IModelApp.viewManager.selectedView;

if (undefined === vp)
    return;

const emph = EmphasizeElements.getOrCreate(vp);
emph.overrideElements(ids, vp, this.getNextColor());
}
</pre></code>
</div>
<br>

</div>

## Instructions for bonus goal

1. Find the method [ColorByCategoryListener.showMessageForCategoryOfSelectedElement](https://github.com/iModeljsJumpStart/challenge-color-by-category/blob/46b662475827c3f25ddfcfafddcc11ad36b661bb/src/frontend/app/ColorByCategory.ts#L78).

2. To complete the bonus, you need to implement both this method and the one above it to find the category name.

3. To show the message, use [MessageManager.outputMessage](https://www.imodeljs.org/reference/ui-framework/notification/messagemanager/outputmessagestatic/) as described [here](https://www.imodeljs.org/learning/ui/framework/notifications/).  The message type OutputMessageType.Toast works nicely for this case.

    If you get stuck <a onclick="toggleHint('hint-2-1')">this hint</a> will help.
<div class="hint" id="hint-2-1" style="display:none">
<code><pre>
const categoryName = "Placeholder";
MessageManager.outputMessage(new ReactNotifyMessageDetails(OutputMessagePriority.Info,
    "Category = " + categoryName, "", OutputMessageType.Toast));
</pre></code>
</div>

4. To query for the category name, look at the other query method in the same file.  Getting the category name requires a join between two tables [bis.SpatialCategory](https://www.imodeljs.org/bis/domains/biscore.ecschema/?term=spatialcategory#spatialcategory) and [bis.GeometricElement3d](https://www.imodeljs.org/bis/domains/biscore.ecschema/?term=spatialcategory#geometricelement3d).

    Try <a onclick="toggleHint('hints-3')">these hints</a> if you get stuck.
<div class="hint-group" id="hints-3" style="display:none">

<a onclick="toggleHint('hint-3-1')">Hint 1</a>
<div class="hint" id="hint-3-1" style="display:none">
Use the property Category.Id on GeometricElement3d.
</div>
<br>

<a onclick="toggleHint('hint-3-2')">Hint 2</a>
<div class="hint" id="hint-3-2" style="display:none">
You need to join the two tables <code>ON</code> the condition that the <code>ecinstanceid</code> of the category is equal to the <code>category.id</code> of the geometric element.
</div>
<br>

<a onclick="toggleHint('hint-3-3')">Hint 3</a>
<div class="hint" id="hint-3-3" style="display:none">
You need to limit the results with a <code>WHERE</code> clause so you consider only the geometric element with the specified inputId.
</div>
<br>

<a onclick="toggleHint('hint-3-4')">Hint 4</a>
<div class="hint" id="hint-3-4" style="display:none">
Use this query:
<code><pre>
const query = `SELECT cat.codeValue categoryName
    FROM bis.SpatialCategory cat
    JOIN bis.geometricElement3d selected ON cat.ecinstanceid = selected.category.id
    WHERE selected.ecinstanceid = ` + inputId;
</pre></code>
</div>
<br>

</div>

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

