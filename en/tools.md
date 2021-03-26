# Tools

To use this tool, [create a personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token). Ensure that this token is NOT shared under any circumstances!

<label for="status-select">Status</label>
<select id="status-select">
    <option value="open">Open</option>
    <option value="closed">Closed</option>
</select>
<label for="repo-select">Project</label>
<select id="repo-select">
    <option value="https://api.github.com/repos/Digital-HR/RecruitmentApp/issues">DND Careers</option>
    <option>HR-GO</option>
</select>
<label for="github-code">Read Only Code</label>
<input id="github-code" type="text" />
<button id="export-btn">Export</button>

## Results
<div>
    <table id="issues-data" class="table wb-tables">
        <thead>
            <tr>
                <th>ID#</th>
                <th>Title</th>
                <th>Labels</th>
                <th>Milestone</th>
            </tr>
        </thead>
        <tbody>
            <th>0</th>
            <td>Sample</td>
            <td>Sample</td>
            <td>Sample</td>
        </tbody>
    </table>
</div>

<script>
    jQuery(document).ready(function($) {
        $("#export-btn").on("click", function() {
            repo = $("#repo-select").val();
            status = $("#status-select").val();
            token = $("#github-code").val();

            project_text = $("#repo-select option:selected").text();

            readIssues(repo + "?per_page=100&page={page}&state=" + status, token, 0);
        });
    });

    issuesList = [];

    function readIssues(project_uri, token, page) {
        $.ajax({
            url: project_uri.replace("{page}", page),
            data: 'data',
            headers: { Authorization: 'Bearer ' + token, Accept: "application/vnd.github.inertia-preview+json" },
            success: function (data) {
                ret = populateIssuesData(data);
                if (ret) {
                    readIssues(project_uri, token, page+1);
                } else {
                    finishData();
                }
            }
        });
    }

    function populateIssuesData(data) {
        ret = false;
        if (data.length > 0) {
            data.forEach(ele => storeData(ele));
            ret = true;
        }
        return ret;
    }

    function storeData(ele) {
        issuesList.push(ele);
    }

    function finishData() {
        issuesList.forEach(function(issue) {
            if (issue.pull_request == undefined) {
                milestone = ""
                if (issue.milestone) {
                    milestone = issue.milestone.title;
                }
                $("#issues-data").append("<tr><th>"+issue.number+"</th><td>"+issue.title+"</td><td>"+getLabels(issue)+"</td><td>"+milestone+"</td></tr>");
            }
        });
        console.log(issuesList);
        console.log("Done!~");
    }

    function getLabels(issue) {
        labels = [];
        issue.labels.forEach(function(label) {
            labels.push("<span style='color:#"+label.color+"'>"+label.name+"<span>");
        });

        return labels.join();
    }
</script>
