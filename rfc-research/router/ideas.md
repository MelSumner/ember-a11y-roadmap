# Ideas

## Post Render
maybe it needs to be done post render?

## Thinking about focus and security
another issue is, focus setting needs to trace back to the click for security- it needs to be tied to the user action. 
There maybe something we are doing with scheduling that is affecting it...Click has an elevated context, security wise. It can schedule things that inherit this - but if we do things that queue and schedule, we could mess that context up. But that would break things like people opening a popup, etc.


