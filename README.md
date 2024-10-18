/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */
var merge = function (intervals) {
    if (!intervals.length) return [];

    // Sort intervals by their start time
    intervals.sort((a, b) => a[0] - b[0]);

    let result = [];

    result.push([intervals[0][0], intervals[0][1]]);

    let lastAddedInterval, curStart, curEnd, prevEnd;
    for (let i = 1; i < intervals.length; i++) {
        lastAddedInterval = result[result.length - 1];

        curStart = intervals[i][0];
        curEnd = intervals[i][1];
        prevEnd = lastAddedInterval[1];

        if (prevEnd >= curStart) {
            // Merge the intervals
            result[result.length - 1][1] = Math.max(curEnd, prevEnd);
        } else {
            // No overlap, just add the interval to the result
            result.push([curStart, curEnd]);
        }
    }
    return result;
};
