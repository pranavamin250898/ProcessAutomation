<!-- README (HTML) -->

<h1>Power Automate Flow – Municipal Comments Classification</h1>

<h2>Overview</h2>
<p>
  This flow automates the processing of municipal planning responses. When a new
  response is submitted (e.g., via Microsoft Forms), the flow retrieves the
  response details, evaluates the comment category (<code>CommentsType</code>),
  and routes the item to the correct branch for downstream actions.
</p>
<p>
  <strong>Based on the option selected in the Microsoft Form, the flow triages
  each submission:</strong> the selected value is stored in
  <code>CommentsType</code>, the <em>Switch</em> evaluates it, and the run
  proceeds through the appropriate branch (Condominium, Site Plan, Subdivision,
  Consent) or defaults to a catch-all path.
</p>

<!-- Optional: include your architecture image -->
<p>
  <em>Architecture Diagram:</em><br>
  <!-- Replace the src with your repo image path, e.g., docs/flow-architecture.png -->
  <img src="https://github.com/pranavamin250898/ProcessAutomation/blob/main/Process%20Automation.png" alt="Flow Architecture Diagram" width="900">
</p>

<hr>

<h2>Flow Architecture</h2>

<ol>
  <li>
    <h3>Trigger — <code>When a new response is submitted</code></h3>
    <ul>
      <li>Starts automatically whenever a user submits a new response through the connected form or data source.</li>
    </ul>
  </li>

  <li>
    <h3>Action — <code>Get response details</code></h3>
    <ul>
      <li>Retrieves all answers from the submission, including the <code>CommentsType</code> field.</li>
      <li>Ensures the latest data is available for routing and processing.</li>
    </ul>
  </li>

  <li>
    <h3>Decision — <code>Switch</code> on <code>CommentsType</code></h3>
    <ul>
      <li>Evaluates the selected comment category and routes the workflow to the appropriate branch.</li>
      <li>Includes a <strong>Default</strong> branch to catch unexpected or empty values.</li>
    </ul>
  </li>
</ol>

<hr>

<h2>Switch Branches</h2>

<table>
  <thead>
    <tr>
      <th>Branch</th>
      <th>Description</th>
      <th>Typical Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Condominium</strong></td>
      <td>Handles responses related to condominium applications.</td>
      <td>1 action (e.g., create SharePoint item or send notification).</td>
    </tr>
    <tr>
      <td><strong>Site Plan</strong></td>
      <td>Processes comments linked to site plan control.</td>
      <td>1 action.</td>
    </tr>
    <tr>
      <td><strong>Subdivision</strong></td>
      <td>Manages feedback about subdivision applications.</td>
      <td>1 action.</td>
    </tr>
    <tr>
      <td><strong>Consent</strong></td>
      <td>Handles consent/severance applications.</td>
      <td>~5 actions (notify stakeholders, save data, generate artifacts, etc.).</td>
    </tr>
    <tr>
      <td><strong>Default</strong></td>
      <td>Catches unrecognized <code>CommentsType</code> values.</td>
      <td>Currently 0 actions — recommended to log/alert for review.</td>
    </tr>
  </tbody>
</table>

<hr>

<h2>Comments Scope</h2>
<p>
  The flow groups related steps inside a <strong>Comments</strong> scope for clarity and maintainability.
  This structure makes it easier to update actions per branch and to troubleshoot failures with
  scoped run-after s
