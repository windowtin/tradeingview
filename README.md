//@version=5
indicator("Fibonacci Retracement with Custom Levels", overlay=true)

// Get the last day's closing price
var float prev_close = na
if (dayofweek != dayofweek[1])  // New day check
    prev_close := close[1]  // Previous day's close

// Define the Fibonacci retracement levels
fibLevels = array.new_float(0)
array.push(fibLevels, 0.0)
array.push(fibLevels, 0.1)
array.push(fibLevels, 0.2)
array.push(fibLevels, 0.236)
array.push(fibLevels, 0.382)
array.push(fibLevels, 0.5)
array.push(fibLevels, 0.618)
array.push(fibLevels, 0.786)
array.push(fibLevels, 1.0)

// Calculate the difference between the previous close and the current price
var float fib_range = na
if not na(prev_close)
    fib_range := high - prev_close

// Plot Fibonacci retracement levels
for i = 0 to array.size(fibLevels) - 1
    level = prev_close + fib_range * array.get(fibLevels, i)
    line.new(bar_index[1], level, bar_index, level, width=2, color=color.new(color.blue, 80))
    label.new(bar_index, level, text="Fib " + tostring(array.get(fibLevels, i)), textcolor=color.white, style=label.style_label_left)

