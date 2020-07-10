# Challenge: Display all user labels associated with spatial elements in a confined cube.

## Summary

By completing this you will learn how to:
- Create a new imodel to be used with the imodel console.
- Query for specific properties in an ECClass.
- Join classes for additional information.
- Add conditions to find specific elements.

## Setup

1) Go to the getting started registration [dashboard](https://www.imodeljs.org/getting-started/registration-dashboard?tab=1) (If you haven't registered yet, please register a new account)
2) Click on "New iModel"
3) Name the imodel whatever you like (i.e. "My House Sample").
4) In the drop down menu, select "House Sample".
5) Click on "submit" and allow the process to complete.
6) Navigate to the [imodel console](https://imodelconsole.bentley.com).
7) Follow the sign in process to gain access to the console.
7) (Optional): Read through the quick tips and do the tutorial.
8) (Optional): If you're not familiar with ECSQL/SQL, check out our [learning page](https://www.imodeljs.org/learning/ecsql/)

## Instructions

Once the setup is complete, we'll need to open the imodel you've just cloned using the imodel console.

### Opening your imodel in the console.

1) Click on your project name in the table under "Listing all Contexts" to display imodels associated with the project
2) Click on your imodel name in the table under "Listing iModels from Project" to display changets associated with the project
3) Click on the named version id to finally open the imodel.

Congratulations! The imodel is now open and ready for queries.

## Steps to complete the challenge

### 1) Begin by listing all EC properties available for all [spatial elements](https://www.imodeljs.org/bis/domains/biscore.ecschema/#spatialelement) in the imodel.

* Write a query to pull all ECProperties from ECClass `Bis.SpatialElement`
* The qualifier for all properties is '`*`'

<a onclick="toggleHint('hint-1-1')">Hint For Step 1</a>
<div class="hint" id="hint-1-1" style="display:none">
The format should look similar to: <code>SELECT ____ FROM ____</code>
</div>

<a onclick="toggleHint('hint-1-2')">Solution Step 1</a>
<div class="hint" id="hint-1-2" style="display:none">
<code>SELECT * FROM Bis.SpatialElement</code>
<br>
</div>

### 2) Instead of displaying all EC properties, write a query that only lists the EC properties we're interested in: "ECInstanceId", "UserLabel" and "Origin"

* ECInstanceId is the `unique` identifier for the element.
* UserLabel is a user created label to describe the element.
* Origin will tell us where the element is in the 3d space.

<a onclick="toggleHint('hint-1-3')">Hint For Step 2</a>
<div class="hint" id="hint-1-3" style="display:none">
The format should look similar to: <code>SELECT ____, ____, ____ FROM ____</code>
</div>

<a onclick="toggleHint('hint-1-4')">Solution Step 2</a>
<div class="hint" id="hint-1-4" style="display:none">
<code>SELECT ECInstanceId, UserLabel, Origin FROM Bis.SpatialElement</code>
<br>
</div>

### 3) While the origin locates where the spatial element is, the size is still unknown. We need to query from the class "Bis.SpatialIndex" for this.

* Write a query (similar to step 1) that lists all information available from the class `Bis.SpatialIndex`
* Class [Bis.SpatialIndex](https://www.imodeljs.org/bis/domains/biscore.ecschema/#spatialindex) contains range information for spatial elements

<a onclick="toggleHint('hint-1-5')">Solution For Step 3</a>
<div class="hint" id="hint-1-5" style="display:none">
<code>SELECT * FROM Bis.SpatialIndex</code>
<br>
</div>

### 4) Notice how SpatialIndex contains the range but it doesn't contain 'UserLabel'. We need to `JOIN` class `Bis.SpatialElement` and class `Bis.SpatialIndex` together.

* Write a query to to display all EC properties from class `Bis.SpatialElement` and `Bis.SpatialIndex` together.
* To join the classes, we need to find the key ECProperty that both classes can `JOIN` on.

<a onclick="toggleHint('hint-1-6')">Hint 1 For Step 4</a>
<div class="hint" id="hint-1-6" style="display:none">
The syntax to join is <code>... FROM Class JOIN OtherClass ON ClassKeyProperty = OtherClassKeyProperty`</code>
</div>

<a onclick="toggleHint('hint-1-7')">Hint 2 For Step 4</a>
<div class="hint" id="hint-1-7" style="display:none">
The joining property key is <code>ECInstanceId</code>. (i.e. <code>Bis.SpatialElement.ECInstanceId</code> and <code>Bis.SpatialIndex.ECInstanceId</code>)
</div>

<a onclick="toggleHint('hint-1-8')">Hint 3 For Step 4</a>
<div class="hint" id="hint-1-8" style="display:none">
The format should look similar to: <br>
<code>SELECT * FROM ____ JOIN ____ ON ____ = ____</code>
</div>

<a onclick="toggleHint('hint-1-9')">Solution For Step 4</a>
<div class="hint" id="hint-1-9" style="display:none">
<code>SELECT * FROM bis.SpatialElement JOIN bis.SpatialIndex ON bis.SpatialElement.ECInstanceId=bis.SpatialIndex.ECInstanceId</code>
<br>
</div>

### 5) Once again the data shown is too verbose. Only pull the information we want to see.

* Write a query to pull only `UserLabel` from `Bis.SpatialElement` and `MinX, MinY, MinZ, MaxX, MaxY, MaxZ` from `Bis.SpatialIndex`
* TIP: We can alias names - instead of writing `bis.SpatialElement.ECInstanceId`, we can write `e.ECInstanceId` if we declare `SELECT ... FROM bis.SpatialElement e`

<a onclick="toggleHint('hint-1-10')">Hint For Step 5</a>
<div class="hint" id="hint-1-10" style="display:none">
The format should look similar to: <br>
<code> SELECT e.____, i.____, i.____, i.____, i.____ FROM ____ e JOIN ____ i ON e.____ = i.____</code>
</div>

<a onclick="toggleHint('hint-1-11')">Solution For Step 5</a>
<div class="hint" id="hint-1-11" style="display:none">
<code>SELECT e.UserLabel, i.MinZ, i.MinY, i.MinZ, i.MaxX, i.MaxY, i.MaxZ FROM bis.SpatialElement e JOIN bis.SpatialIndex i ON e.ECInstanceId=i.ECInstanceId</code>
<br>
</div>

### 6) Now that we have all the information we need, it's time to add a simple condition.

* Write a query with the WHERE clause to show only spatial elements that have a MinX >= 5 AND MinY >= 6.
* The format for WHERE clause is `FROM ... WHERE ... AND ...`

<a onclick="toggleHint('hint-1-12')">Hint For Step 6</a>
<div class="hint" id="hint-1-12" style="display:none">
The format should look similar to: <br>
<code> SELECT e.____, i.____, i.____, i.____, i.____ FROM ____ e JOIN ____ i ON e.____ = i.____ WHERE i.___ >= 5 AND i.___ >= 6</code>
</div>

<a onclick="toggleHint('hint-1-13')">Solution For Step 6</a>
<div class="hint" id="hint-1-13" style="display:none">
<code>SELECT e.UserLabel, i.MinZ, i.MinY, i.MinZ, i.MaxX, i.MaxY, i.MaxZ FROM bis.SpatialElement e JOIN bis.SpatialIndex i ON e.ECInstanceId=i.ECInstanceId WHERE i.MinX >= 5 AND i.MinY >= 6 </code>
<br>
</div>

### 7) The final challenge is to retrieve the user labels of all spatial elements that are contained in a cube with the minimum bounding coordinate at (5, 6, 6) and maximum bounding coordinate at (15, 15, 14).

* (X, Y, Z) are cartesian coordinates.

<a onclick="toggleHint('hint-1-14')">Solution For Challenge</a>
<div class="hint" id="hint-1-14" style="display:none">
<code> SELECT e.UserLabel, i.MinZ, i.MinY, i.MinZ, i.MaxX, i.MaxY, i.MaxZ FROM bis.SpatialElement e JOIN bis.SpatialIndex i ON e.ECInstanceId=i.ECInstanceId WHERE i.MinX >= 5 AND i.MinY >= 6 AND i.MinZ >= 6 AND i.MaxX <= 15 AND i.MaxY <= 15 AND i.MaxZ <= 14</code>
<br>
</div>

## Conclusion

So, were you up to the challenge? Feel free to explore the console and experiment with your own queries. You can learn much more about how ECSQL queries work [here](https://www.imodeljs.org/learning/ecsql/).

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