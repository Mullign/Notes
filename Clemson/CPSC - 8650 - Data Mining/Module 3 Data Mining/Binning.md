![[Binning Slides.pdf]]Simple discretization, meaning binning, okay? Binning has two methods. One is called equal weights or equal distance addition. So you divide the range. So you are dividing the range, not the divide the data value here, okay? You divide the range into n intervals of equal size. So essentially you are making the uniform grid. 

For example, if you have a maximum and a minimum, right? So for example, A is the lowest, and B is the highest value of the attribute. Then the interval weight of this bin becomes B minus A divided by the number of n, okay? So because you have n intervals, okay? So for example, you have a data range from 1 to 100, assume, okay? Then what you can do is say, hey, you have 2,000 data, okay? So what you can do is you take, say, I want to binning into 10 bins. 

So then what you can do is add 100 minus 0 and divide it by 10. That is the data range. So for each interval is 10, 10, 10, 10, 10, okay? So this is a very straightforward approach. Of course, the outliners may dominate the presentation. For example, all the data here, right? What if you have majority of your data is below 10, okay? 

And then there is one data at 99. So what happens, you will have one bin with everything. And then the rest of the bin has nothing, but only the last bin has one point, okay? So it cannot handle such skewed data, okay? So to solve the problem, you can also do the equal depth. Well, you try to put each bin has an equal number of values. So you divide the data range into n intervals, okay? 

They will each contain approximately same number of samples. So for example, you have 2,000 samples, right? Like the example we talked about. And even though you have 100, data range is 1 to 100. Now you want to create the 10 bins. So what you do is you take the data, right? And the first 200 data, put it in one bin. 

The next 200 data, put it in a second bin. The next 200 data, put it in a third bin and continue going forward. And then you put all data into those 10 bins and make sure that each bin has the equal number because you have 2,000 here. So 2,000 can be divided by 10, right? But anyhow, you want to make each bin contain approximately the same number of samples. So this is a good depth scaling. But you may have problem in handling the categorical attributes, okay? 

Because the categorical attributes, like you have different categories. So the data value are just the categories, okay? If you do such a, even though you do the, you order these categorical, okay, data. Then if you do the equal frequency here, the problem is that it is possible you put one bin with two or three different categories. Or you may split one category into different bins. So this is a little bit tricky if you want to do an equal depth, okay? So let's get some example here, okay? 

So you have sorted the data in dollars as the price, okay? So you can say 4, 8, 9, 10, 15, and then goes 34. So first we take equal frequency, okay? And so, now after we do the bin, we want to do a smoothing as well, okay? So we can do the smoothing. Now, bin method, after we use it, and we can do the smooth, okay? So you can see you partition into equal frequency, right? 

And then equal frequency here, that 4, 8, 9, 15, 21, 21, 24, 15, right? And then 26, 28. So each one has four values because we take a three bin. So assume we use a three bin, okay? So after that, we can take a bin mean value, okay? So we calculate the bin mean value, and then we get it. And then we replace all the data with the bin mean value, okay? 

So this is one method, okay? So what do you get is you reduce the data size to three bins. Each bin include only one value, okay? So that is called a smooth. You smooth the value. So you get a bin, 9, and then you get an extra 23, get a next number, 29. You can also smooth in by bin boundary where you have two values. 

One is the lower boundary of that bin, and another is the higher value of that bin. So depend on your actual value. If your actual value is closer to the lower value, then use the lower value. And if your actual value is closer to the higher value, and then do the higher value, okay? So that's it. And then you can for this, for this data set, if you use the equal, here we use equal frequency, right? Equal that. 

If you use the equal width, then what do you do is you take the, you take a three range, right? So you take 34 minus four equal to 30, divide by three. Again, the same three bin. So what you will get that from four to, so 34, that's a three, 10. So the first step is the 10. So four to 14, right? And then 15 to 25, okay? 

36 to 34. Or actually you can do four to 13, okay? And then 14 to 23, and 24 to 34. So you do this, okay? So basically you make it equal width, okay? And so four to 14, 14 to 24, 24 to 34. So you make that range. 

And then you put the data in there, okay?