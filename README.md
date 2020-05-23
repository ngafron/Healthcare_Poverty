Healthcare vs. Poverty

Description:
Create a scatter plot between two of the data variables such as Healthcare vs. Poverty utilizing d3 skills and data from the given csv file. Utilize HTML, CSS, Javascript, and D3

Correlations Discovered Between Health Risks Income:
    Based on the scatter plot, one can infer that as the poverty level increases, the number of individuals without healthcare generally     increases. There are some outliers in the dataset but by observing the plot, there seems to be a positive correlation between the       poverty percentage and the lacks healthcare percentage.

    It would seem based on the data, that Texas is the major outlier in the dataset.  Although there are several states with a higher       percentage of poverty, Texas is the leading state in terms of citizens lacking healthcare on a percentage basis.  There seems to be     other forces at play but more research is needed to determine the cause.
```
d3.csv("assets/data/data.csv").then(function(health_data) {

    health_data.forEach(function(data) {
        data.healthcare = +data.healthcare;
        data.poverty = +data.poverty;
        data.abbr = data.abbr;
    });

    var xLinearScale = d3.scaleLinear()
        .domain([4, d3.max(health_data, d => d.healthcare)])
        .range([0, width]);

    var yLinearScale = d3.scaleLinear()
        .domain([8, d3.max(health_data, d => d.poverty)])
        .range([height, 0]);

    var bottomAxis = d3.axisBottom(xLinearScale);
    var leftAxis = d3.axisLeft(yLinearScale);

    chartGroup.append("g")
        .attr("transform", `translate(0, ${height})`)
        .call(bottomAxis);

    chartGroup.append("g")
        .call(leftAxis);

    chartGroup.selectAll("circle")
    .data(health_data)
    .enter()
    .append("circle")
    .attr("cx", d => xLinearScale(d.healthcare))
    .attr("cy", d => yLinearScale(d.poverty))
    .attr("r", "15")
    .attr("fill", "pink")
    .attr("opacity", ".5");

    chartGroup.select("g")
    .selectAll("circle")
    .data(health_data)
    .enter()
    .append("text")
    .text(d => d.abbr)
    .attr("x", d => xLinearScale(d.healthcare))
    .attr("y", d => yLinearScale(d.poverty))
    .attr("dy",-415)
    .attr("text-anchor", "middle")
    .attr("font-size", "12px")
    .attr("fill", "black");

    chartGroup.append("text")
    .attr("transform", "rotate(-90)")
    .attr("y", 0 - margin.left + 40)
    .attr("x", 0 - (height / 2))
    .attr("dy", "1em")
    .attr("class", "axisText")
    .text("In Poverty (%)");

    chartGroup.append("text")
    .attr("transform", `translate(${width / 2}, ${height + margin.top + 30})`)
    .attr("class", "axisText")
    .text("Lacks Healthcare (%)");
}).catch(function(error) {
  console.log(error);
});
```
