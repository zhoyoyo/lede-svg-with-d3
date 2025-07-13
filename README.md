# Lede 2025 Storytelling: Create SVG with D3

An 8-step guide to create a simple SVG graphic with D3.js

#### What to do before we start:
- Clone this repo to your computer (not sure how to? check it out [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)) or download the zip file to this repo using the green top button that says `CODE` 
- Navigate to the repo with terminal, and load a local server. 
     - For all VS Code users, check out this plugin: [How to load changes spontanously on your local server with VS Code](https://www.freecodecamp.org/news/vscode-live-server-auto-refresh-browser/) 
     - If you use Node or would like to learn (because it's so useful), check out [http-server](https://www.npmjs.com/package/http-server)
     - You can use the following line if you use python. Once it says a local server is running, type in `localhost:8080` on your browser. You should see the content of the `index.html` page there!
        ```
        python3 -m http.server --cgi 8080
        ```
   

## Preparation

1. Create a basic html page. If you don't know how, refers to Soma’s tutorial: [How to create and host a web pages on Github](https://jonathansoma.com/fancy-github/github-pages/). For this tutorial, we will use `index.html` as a starter. 


2. Add the d3 library to the page. For the purpose of this demo, we are loading the entire D3 library in one Javascript (js) file.  Add the following script to your HTML markup. 


    ```
    https://cdnjs.cloudflare.com/ajax/libs/d3/7.8.5/d3.min.js
    ```


3. Add data variables. For this demo, we will use Jeff Bezos' wedding cost data.
    - You will be doing this inside the `script` tag inside `head`.

```
// unit in million
const bezosCost = 56, bezosWealth = 236000;
const averageCost = 0.033, averageWealth = 0.1929;

```

## Transform data into usable scales

4. Use `d3.scaleSqrt` ([🔗 to doc](https://observablehq.com/@d3/continuous-scales)) to calculate the appropriate radius based on values.  

```
// let's assume we want the max radius of the circles to be 100
const scaleRadius = d3.scaleSqrt().domain([0, bezosWealth]).range([0, 100]);

```

## Create web elements and bind data to them

5. Create an overall SVG container for your graphic inside `#my-svg-chart` using `d3.select().append()`
    - Make sure you declare `width` and `height` for your SVG element with the chained `.attr()` function.
        
        ```
        const myChart = d3
                .select('#my-svg-chart')
                .append('svg')
                .attr('width', 640)
                .attr('height', 640)
        ```


6. Create shapes that you want to bind your data to, and bind the data to them. You will be using `d3.selectAll().data().join()`. 
    - You can create:
        - [Circles](https://www.w3schools.com/graphics/svg_circle.asp)
        - [Rectangles](https://www.w3schools.com/graphics/svg_rect.asp)
        - [Lines](https://www.w3schools.com/graphics/svg_line.asp)
        - [Text](https://www.w3schools.com/graphics/svg_text.asp)
        - ... (any other SVG elements)

    - This code example uses a rectangle.

        ```
        const circles = myChart
            .selectAll('circle')
            .data([circleData])
            .join('circle');
        ```

## Manipulate the elements using attributes and styles 

7. Tweak the attributes of the SVG shapes to position them at the right places.


    ```
    // with SVG circle-specific attributes

    circles
        .attr('cx', xPos)
        .attr('cy', 100)
        .attr('r', (d) => scaleRadius(d))

    ```

8. Change the style attributes of the SVG shapes to achieve desired effects

    ```
    // this creates alternating colors based on the index of the circle

    circles
        .style('fill', function(d,i) {
          return i%2 == 0 ? '#ccc' : 'red'
        })

    ```

You're done. Good job.

You can play around different SVG shapes/text/path, different ways of encoding your data...  
- Use squares, bars instead of circles? 
- Encode data as colors instead of shapes? 
- Use a different dataset to create a different effect? 

... and don't forget to publish your page.


--- 

#### Additional resources on D3
- [Read the official doc](https://d3js.org/getting-started) and [the most important API](https://github.com/d3/d3/blob/main/API.md)
- [D3 gallery on Observable](https://observablehq.com/@d3/gallery) if you want to play around/ borrow the code.  
- [How to learn D3?](https://2019.wattenberger.com/blog/d3) An interactive tutorial by Amelia Wattenberger
- [Shirley Wu's Introduction to D3](https://observablehq.com/@sxywu/introduction-to-svg-and-d3-js?collection=@sxywu/introduction-to-d3-js), also on Observable
