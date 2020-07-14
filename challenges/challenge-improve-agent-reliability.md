# Challenge: Improve Your iModel.js Agent's Reliability!

## Summary

By completing this you will learn how to:
- Make your iModel.js agent more resilient to errors and scheduled maintenance.

## Setup

1. Install the [required tools](https://www.imodeljs.org/getting-started/)

2. Clone the [jumpstart-agent repo](https://github.com/iModeljsJumpStart/jumpstart-agent)

3. Follow the setup instructions in the jumpstart-agent [README](https://github.com/iModeljsJumpStart/jumpstart-agent/blob/master/README.md)

## Goals

**Goal** Follow the instructions to update the agent so you never miss an iModelHub event.

**Bonus** Create a new "start:prod" npm script to automatically restart the agent anytime a fatal error occurs.
## Solution

The best way to learn is by doing!  But, if you want to skip ahead you can go right to the [full solution](https://github.com/iModeljsJumpStart/jumpstart-agent/tree/challenge-solution).

## Instructions

1. Update `MyAgent.ts` to reuse an existing iModelHub subscription ID (only creating a new event subscription in iModelHub when necessary).

    If you need help try <a onclick="toggleHint('hints-1')">these hints</a>.
    <div class="hint-group" id="hints-1" style="display:none">

    <a onclick="toggleHint('hint-1-1')">Hint 1</a>
    <div class="hint" id="hint-1-1" style="display:none">
    Subscriptions are created in the <a href="https://github.com/imodeljs/agent-starter/blob/c81bbe0ea49af7abbb6c4b4962dbc8fd2f158262/src/MyAgent.ts#L35">listen method</a>.
    </div>
    <br>

    <a onclick="toggleHint('hint-1-2')">Hint 2</a>
    <div class="hint" id="hint-1-2" style="display:none">
    You can read and write the subscription ID to a local file
    </div>
    </div>

2. Update `MyAgent.ts` to never delete the iModelHub subscription.

    If you need help try <a onclick="toggleHint('hints-2')">these hints</a>.
    <div class="hint-group" id="hints-2" style="display:none">

    <a onclick="toggleHint('hint-2-1')">Hint 1</a>
    <div class="hint" id="hint-2-1" style="display:none">
    Subscriptions are created in the <a href="https://github.com/imodeljs/agent-starter/blob/c81bbe0ea49af7abbb6c4b4962dbc8fd2f158262/src/MyAgent.ts#L90">terminate method</a>.
    </div>
    </div>
    
3. Test out your new behavior!
    - Start your agent via `npm start`, wait for it to begin listening, and then stop it.
    - While your agent is ***stopped***, synchronize new changes via the iTwin Synchronizer.
    - Re-start your agent (`npm start`) _after_ iTwin Synchronizer has finished pushing the changeset(s).
    - If you completed steps 1 & 2 correctly, your agent will pick right up where it left off and see the event it missed!

4. (Bonus) Create a new `start:prod` npm script in `package.json` to automatically restart the agent anytime a fatal error occurs.

    If you need help try <a onclick="toggleHint('hints-3')">these hints</a>.
    <div class="hint-group" id="hints-3" style="display:none">

    <a onclick="toggleHint('hint-3-1')">Hint 1</a>
    <div class="hint" id="hint-3-1" style="display:none">
    You can use the <a href="https://www.npmjs.com/package/forever">forever</a> npm package here.
    </div>
    </div>
## Conclusion

So, were you up to the challenge? Check out how we solved it by viewing our [full solution](https://github.com/iModeljsJumpStart/jumpstart-agent/tree/challenge-solution).  Let us know if you have a better way.

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
