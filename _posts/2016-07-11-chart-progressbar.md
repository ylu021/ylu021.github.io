---
title: ProgressBar.js Doughnut Chart
layout: post
category: JS
tags: chart
---
---

# code

           // progressbar.js@1.0.0 version is used
           // Docs: http://progressbarjs.readthedocs.org/en/1.0.0/
           // drawChart('By You', chart1, i1);
           // drawChart('By Others', chart2, i2);

           function drawChart(str,id,val){
                var bar = new ProgressBar.Circle(id, {
                  color: '#373f51',
                  // This has to be the same size as the maximum width to
                  // prevent clipping
                  strokeWidth: 4,
                  trailWidth: 4,
                  easing: 'easeInOut',
                  duration: 1400,
                  text: {
                    autoStyleContainer: false
                  },
                  from: { color: '#a9bcd0', width: 4 },
                  to: { color: '#a9bcd0', width: 4 },
                  // Set default step function for all animate calls
                  step: function(state, circle) {
                    circle.path.setAttribute('stroke', state.color);
                    circle.path.setAttribute('stroke-width', state.width);

                    var value = Math.round(circle.value() * 100);
                    if (value === 0) {
                      circle.setText('');
                    } else {
                      circle.setText('<center>'+value+'%</center>\n'+str);
                    }

                  }
                });
                // bar.text.style.fontFamily = '"Raleway", Helvetica, sans-serif';
                bar.text.style.fontSize = '1rem';
                bar.text.style.lineHeight = '30px';
                var value = val/total;
                bar.animate(value);  // Number from 0.0 to 1.0
           } //for progressbar
