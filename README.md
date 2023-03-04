<!--
@onload

if(!window.SCORE) {
    window.SCORE = 0
}
if(window.SCORE) {
    window._SCORE = window.SCORE
}

if (!window.SCORE_observer) {
    window.SCORE_observer = {}
}

// Define a property getter and setter for the global variable
Object.defineProperty(window, 'SCORE', {
  get: function() {
    return this._SCORE;
  },
  set: function(newValue) {
    this._SCORE = newValue;
    for (let id in window.SCORE_observer) {
        window.SCORE_observer[id](newValue);
    }
  }
});
@end

@score: @_score(@uid,@0)

@_score
<script style="display: block" modify="false" run-once>
function update(score) {
  const gauge = {
    tooltip: {
        formatter: '{a} <br/>{b} : {c}%'
    },
    series: [
        {
        name: 'Progress',
        type: 'gauge',
        progress: {
            show: true
        },
        detail: {
            valueAnimation: true,
            formatter: '{value}'
        },
        data: [
            {
                value: score,
                name: '@1'
            }
        ]
        }
    ]
    };

  send.lia(`HTML: <lia-chart option='${JSON.stringify(gauge)}'></lia-chart>`)
}

const id = "@0"

if (!window.SCORE_observer) {
    window.SCORE_observer = {}
}
window.SCORE_observer[id] = update

update(window.SCORE || 0)
</script>
@end
-->

# SCORM-Progress

Little observer example for visualizing SCORM progress. If not in Scorm, use the interactive script to change the SCORE value ...

``` js
window.SCORE = 0.1
```
<script>@input</script>

@score(Progress)

@score(Fortschritt)

## Another page example

@score(Punkte)

## Implementation

``` html
<!--
@onload

if(!window.SCORE) {
    window.SCORE = 0
}
if(window.SCORE) {
    window._SCORE = window.SCORE
}

if (!window.SCORE_observer) {
    window.SCORE_observer = {}
}

// Define a property getter and setter for the global variable
Object.defineProperty(window, 'SCORE', {
  get: function() {
    return this._SCORE;
  },
  set: function(newValue) {
    this._SCORE = newValue;
    for (let id in window.SCORE_observer) {
        window.SCORE_observer[id](newValue);
    }
  }
});
@end

@score: @_score(@uid,@0)

@_score
<script style="display: block" modify="false" run-once>
function update(score) {
  const gauge = {
    tooltip: {
        formatter: '{a} <br/>{b} : {c}%'
    },
    series: [
        {
        name: 'Progress',
        type: 'gauge',
        progress: {
            show: true
        },
        detail: {
            valueAnimation: true,
            formatter: '{value}'
        },
        data: [
            {
                value: score,
                name: '@1'
            }
        ]
        }
    ]
    };

  send.lia(`HTML: <lia-chart option='${JSON.stringify(gauge)}'></lia-chart>`)
}

const id = "@0"

if (!window.SCORE_observer) {
    window.SCORE_observer = {}
}
window.SCORE_observer[id] = update

update(window.SCORE || 0)
</script>
@end
-->
```



