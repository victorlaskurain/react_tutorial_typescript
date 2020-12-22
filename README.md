# Function style react componets + typescript

A version of the React tutorial slightly modified to use only function style components and Typescript's static type checking. The main benefit of using Typescript instead of plain Javascript is the added safety derived from Typescript's extensive type checking.

After adding Typescript to the project all you need to do in order to use Typescript with React is adding type annotations to your functions. Typescript can infer most of the rest of the types. For example, this function:

```javascript
function Square(props) {
```

would turn into this:

```typescript
type SquareValue = 'X'|'O'|null;

interface SquareProps {
    onClick: () => void,
    value: SquareValue
}
function Square(props: SquareProps) {
```

Remember that this is information you already have to take into account: if you fail to pass the value prop the Square component you will get a runtime error. By providing the compiler with this information you can turn a runtime error into a compile time error. Moreover, the runtime errors might not arise in every run of the application and might even be rather hard to see at glance. On the other hand, the compiler will always warn you of them. Let's say that you forgot that setState does not merge and thus left out ```...state``` thus typing this:

```typescript
    function jumpTo(step: number) {
        setState(state => { return {
            stepNumber: step,
            xIsNext: (step % 2) === 0
        }});
    }
```

instead of this:

```typescript
    function jumpTo(step: number) {
        setState(state => { return {
            ...state,
            stepNumber: step,
            xIsNext: (step % 2) === 0
        }});
    }
```

At runtime the jump to buttons would stop working but the error would not show up until someone clicked on of the buttons. Instead, the compiler will spit something like this into your face:

```
    Property 'history' is missing in type '{ stepNumber: number; xIsNext: boolean; }' but required in type '{ history: { squares: SquareValue[]; }[]; xIsNext: boolean; stepNumber: number; }'.  TS2345

    74 |     }
    75 |     function jumpTo(step: number) {
  > 76 |         setState(state => { return {
       |                  ^
    77 |             stepNumber: step,
    78 |             xIsNext: (step % 2) === 0
    79 |         }});
```

Type checking also works inside JXP. For example if you type this (note the typo "ssquare":

```typescript
                    <Board ssquares={current.squares}
                           onClick={(i) => handleClick(i) } />
```

The compiler will tell you something along these lines:

```
  Property 'ssquares' does not exist on type 'IntrinsicAttributes & BoardProps'. Did you mean 'squares'?  TS2322

    105 |             <div className="game">
    106 |                 <div className="game-board">
  > 107 |                     <Board ssquares={current.squares}
        |                            ^
    108 |                            onClick={(i) => handleClick(i) } />
    109 |                 </div>
    110 |                 <div className="game-info">
```

# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
