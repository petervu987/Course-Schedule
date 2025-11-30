# Course-Schedule

class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> graph(numCourses);
        vector<int> indegree(numCourses, 0);

        for (auto &p : prerequisites) {
            int c = p[0];
            int pre = p[1];
            graph[pre].push_back(c);
            indegree[c]++;
        }

        queue<int> q;
        for (int i = 0; i < numCourses; i++) {
            if (indegree[i] == 0)
                q.push(i);
        }

        int take = 0;

        while (!q.empty()) {
            int curr = q.front();
            q.pop();
            take++;

            for (int next : graph[curr]) {
                indegree[next]--;
                if (indegree[next] == 0)
                    q.push(next);
            }
        }

        return take == numCourses;
    }
};
