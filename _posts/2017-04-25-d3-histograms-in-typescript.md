---
layout: post
title:  Drawing histograms using D3 and typescript
date:   2017-04-25 01:00:00 +1100
category: software development
tags: [typescript, angular, d3, histogram]
---

# Drawing histograms using D3 and typescript

If you ever played with D3, you've most likely found [https://bl.ocks.org](https://bl.ocks.org) - Mike Bostock's site where he explains how to draw D3 charts from a very basic to quite complex ones.

On several occasions I used his examples to draw charts on my sites. However, recently i got into several problems when switching to TypeScript.

In order to save you struggle with porting Mike's samples here's [the histogram from his site](https://bl.ocks.org/mbostock/3048450]) translated to TypeScript and wrapped in an Angular2 component.

Click [here to find a GIST](https://gist.github.com/random82/79a1bfe61e2243ea7bdf0e5370d169e3#file-histogram-component-ts) with the full source code

## Prerequisites

In order to add this example to your TS app you'll need following packages:

```
npm install d3-axis d3-random d3-scale d3-selection --save
```

## Differences between JS and TS code

### Imports

This example follows the modular approach for D3 v4. Finding the correct module to import is a matter of going to [D3 v4 API reference](https://github.com/d3/d3/blob/master/API.md) and finding which d3-x module contains types you need.

```typescript
import { select } from 'd3-selection';
import { scaleLinear } from 'd3-scale';
import { range, histogram, max } from 'd3-array';
import { format } from 'd3-format';
import { randomBates } from 'd3-random';
import { axisBottom } from 'd3-axis';
```

### Using TS generics properly

When using TypeScript we need to specify types we use in generic classes.

And JavaScript like this


```javascript
var x = d3.scaleLinear().rangeRound([0, width]);
```

becomes

```typescript
let x = scaleLinear<number>().rangeRound([0, width]);
```

### Avoding minor @types issues

For the d3-array version 1.2.0 passing ```x.domain()``` as ```histogram.domain()``` argument, raises a type error.

After drilling into d3-array.ts.d definition I've found this:

```typescript
interface Histogram<T> {
    /* REMOVED FOR BREVITY */

    /**
    * 2: numeric data → [min, max]
    * @link https://github.com/d3/d3-array#histogram_domain
    */
    // SOMEDAY => any → => $$.Orderable
    domain():(values:$$.Orderable[]) => any;
    domain(value:[$$.Orderable, $$.Orderable]):this;
    domain(value:(values:$$.Orderable[]) => any[]):this;

    /* REMOVED FOR BREVITY */
}
```

So, I've decide to go with the third option and...

```javascript
var bins = d3.histogram()
              .domain(x.domain())
              .thresholds(x.ticks(20))
```

became

```typescript
let generator = histogram<number>()
                .domain(d => x.domain())
                .thresholds(x.ticks(20));
```

## Extra - using Angular2 component template with D3

In order to use D3 to modify part of your Angular template DOM, you'll need to use ```ElementRef``` to pass the template into your component code.

```typescript
import { Component, OnInit, ElementRef } from '@angular/core';
import { select } from 'd3-selection';

@Component({
    selector:'histogram',
    template:'<h1>Hello histogram</h1>\
              <svg id="hist" width="960" height="500"></svg>'
})
export class HistogramComponent implements OnInit {

    el: HTMLElement;

    constructor(private elementRef: ElementRef){
        this.el = elementRef.nativeElement;
    }

    ngOnInit(): void {
        this.drawHistogram();
    }

    drawHistogram(){
        let hist = select(this.el).select('#hist');
        // Follow with your regular D3 flow
    }
```


Click [here to find a GIST](https://gist.github.com/random82/79a1bfe61e2243ea7bdf0e5370d169e3#file-histogram-component-ts) with the full source code

