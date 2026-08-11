```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <title>Stacking Context Playground</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #eee;
    }

    /*
      OUTSIDE ELEMENT
      Try changing this z-index.
    */
    .outside {
      position: fixed;
      top: 100px;
      left: 250px;

      width: 300px;
      height: 200px;

      background: rgba(255, 0, 0, 0.7);

      z-index: 30;

      display: flex;
      align-items: center;
      justify-content: center;
    }

    /*
      PARENT
      This creates a stacking context because:
      position: fixed + z-index: 20
    */
    .parent {
      position: fixed;
      top: 150px;
      left: 100px;

      width: 400px;
      height: 300px;

      background: rgba(0, 0, 255, 0.7);

      z-index: 20;

      padding: 40px;
    }

    /*
      MIDDLE
      Doesn't create a stacking context in this example.
    */
    .middle {
      width: 300px;
      height: 220px;

      background: rgba(0, 255, 0, 0.6);

      padding: 30px;
    }

    /*
      CHILD
      Change this z-index and experiment.

      IMPORTANT:
      z-index does NOTHING here because
      the element is not positioned.
    */
    .child {
      width: 200px;
      height: 150px;

      background: rgba(255, 255, 0, 0.8);

      z-index: 999;

      display: flex;
      align-items: center;
      justify-content: center;
    }
  </style>
</head>

<body>

  <!-- This is outside the parent stacking context -->
  <!-- <div class="outside">
    OUTSIDE<br />
    z-index: 30
  </div> -->

  <!-- Parent stacking context -->
  <div class="parent">
    PARENT<br />
    z-index: 20

    <div class="middle">
      MIDDLE

      <div class="child">
        CHILD<br />
        z-index: 999
      </div>
    </div>
  </div>

</body>

</html>
```