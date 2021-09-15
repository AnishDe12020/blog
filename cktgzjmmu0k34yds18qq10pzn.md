## Easter eggs using React Rooks

I stumbled upon this great React Hooks library called [Rooks](https://react-hooks.org/) recently and it has got a lot to offer. We all have discovered various Easter eggs in various apps and sites. It can range anywhere from stumbling upon a Rick-roll when you click a button a certain number of times or enjoying playing snake when you press a hidden button on a 404 page. 

Ok, so let us start making an Easter egg 🥚

### An alert when you press a certain key combination

Rooks provides us with a very useful [useKeys hook](https://react-hooks.org/docs/useKeys). With this, we can trigger an action whenever a certain key combination is pressed. For this example whenever the keys Q, W, E, R, T, and Y are pressed, all together, an alert will be triggered saying the key combination was pressed. This is a simple example and hence a great place to start

Firstly we need to create a react project (you can use Gatsby, NextJS, etc as well as long as it is React). I am using [Codesandbox](https://codesandbox.io/) for this tutorial but you can do it locally as well. 

Now we need to install rooks so we can run 
```
npm i - s rooks
```
You can following the [getting started guide](https://react-hooks.org/docs/getting-started/) for rooks.

Now let us see the code

Firstly, we need to import the hook:
```js
import { useKeys } from "rooks";
```

Now we need to configure the hook:

```js
useKeys(["KeyQ", "KeyW", "KeyE", "KeyR", "KeyT", "KeyY"], () => {
    alert("QWERTY");
});
```

Here, the first parameter is an array of all the keys that need to be pressed. We pass in a callback function which will be triggered if all the keys are pressed as the second parameter. 

Now whenever the 6 keys are pressed together, we will see this alert - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631436265132/OOazJ3pmE.png)

Codesandbox - 

%[https://codesandbox.io/embed/weathered-wave-gy3s3?fontsize=14&hidenavigation=1&theme=dark]

Now we have successfully made our first Easter egg 🥳!!!

Now it is time for you to explore other [hooks](https://react-hooks.org/docs/hooks-list/) and come up with some great Easter eggs for your site.

Feel free to share your creations down in the comments section.



