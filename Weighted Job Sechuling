/*
    Time Complexity: O(N*log(N))
    Space Complexity: O(N)

    Where N is the number of jobs.
*/

#include <algorithm>

struct job
{
    int startTime;
    int endTime;
    int jobProfit;
};

bool compare(job a, job b)
{
    return a.endTime < b.endTime;
}

// Function to find the latest non conflicting job.
int nonConflictingJob(vector<job> &jobs, int i)
{
    int s = 0;
    int e = i - 1;
    int ans = -1;

    while (s <= e)
    {
        int mid = (s + e) / 2;

        if (jobs[mid].endTime <= jobs[i].startTime)
        {
            ans = mid;
            s = mid + 1;
        }
        else
        {
            e = mid - 1;
        }
    }

    return ans;
}

long long int findMaxProfit(vector<int> &start, vector<int> &end, vector<int> &profit)
{
    int n = start.size();

    // Creating jobs array of size N.
    vector<job> jobs(n);

    for (int i = 0; i < n; i++)
    {
        jobs[i].startTime = start[i];
        jobs[i].endTime = end[i];
        jobs[i].jobProfit = profit[i];
    }

    // Sorting the jobs in the increasing order of end time.
    sort(jobs.begin(), jobs.end(), compare);

    // Creating a dp array of size N.
    vector<long long int> dp(n);

    dp[0] = jobs[0].jobProfit;

    for (int i = 1; i < n; i++)
    {
        // First calculating the profit by excluding the current job.
        long long int excProfit = dp[i - 1];

        // Then, calculating the profit by including the current job.
        long long int incProfit = jobs[i].jobProfit;

        // Finding the index of closest non conflicting job to current job.
        int index = nonConflictingJob(jobs, i);

        // If the index is not equal to -1, adding the profit of that job.
        if (index != -1)
        {
            incProfit += dp[index];
        }

        // Updating the dp array.
        dp[i] = max(incProfit, excProfit);
    }

    return dp[n - 1];
}

