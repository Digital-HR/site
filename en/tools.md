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
                <th>Created By</th>
            </tr>
        </thead>
        <tbody>
            <th>0</th>
            <td>Sample</td>
            <td>Sample</td>
            <td>Sample</td>
            <td>Sample</td>
        </tbody>
    </table>
</div>

{% include tools.html %}

