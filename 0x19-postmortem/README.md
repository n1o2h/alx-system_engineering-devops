
    <h1>Postmortem Report: Naklla Application Outage</h1>

    <h2>Issue Summary</h2>
    <p><strong>Duration of Outage:</strong><br>
    Start Time: June 21, 2024, 14:00 UTC<br>
    End Time: June 21, 2024, 17:30 UTC</p>

    <p><strong>Impact:</strong><br>
    During the outage, the Naklla application, which organizes public transport including buses, school buses, private buses, and taxis, experienced significant slowdowns and intermittent downtime. Users reported issues with accessing real-time bus information, booking taxis, and managing subscriptions. Approximately 65% of our user base was affected, leading to substantial disruptions in their daily commutes and transportation planning.</p>

    <p><strong>Root Cause:</strong><br>
    The root cause of the outage was a misconfiguration in the load balancer settings, which led to uneven distribution of traffic across our servers. This caused some servers to become overloaded while others remained underutilized, leading to performance degradation and intermittent downtime.</p>

    <div class="image">
        <img src="#" alt="Naklla Outage">
    </div>

    <h2>Timeline</h2>
    <div class="timeline">
        <ul>
            <li><strong>14:00 UTC:</strong> Issue detected through an automated monitoring alert indicating high response times and increased error rates.</li>
            <li><strong>14:05 UTC:</strong> Engineering team begins investigating the alert, initially suspecting a database issue due to high query times.</li>
            <li><strong>14:20 UTC:</strong> Further investigation shows that database performance is normal; attention shifts to application servers.</li>
            <li><strong>14:45 UTC:</strong> Misleading debug path: suspecting a potential memory leak in the application code.</li>
            <li><strong>15:10 UTC:</strong> Escalated to the infrastructure team after application code issues are ruled out.</li>
            <li><strong>15:30 UTC:</strong> Infrastructure team identifies unusual traffic patterns on the load balancer.</li>
            <li><strong>15:45 UTC:</strong> Root cause identified as a misconfiguration in the load balancer settings.</li>
            <li><strong>16:00 UTC:</strong> Configuration changes are made to redistribute traffic evenly across servers.</li>
            <li><strong>16:30 UTC:</strong> Monitoring shows gradual improvement in response times and error rates.</li>
            <li><strong>17:30 UTC:</strong> Full recovery confirmed, with all services operating normally.</li>
        </ul>
    </div>

    <div class="image">
        <img src="#" alt="Timeline">
    </div>

    <h2>Root Cause and Resolution</h2>
    <p><strong>Root Cause:</strong><br>
    The load balancer was configured with incorrect weight settings for server instances, causing disproportionate traffic distribution. Some servers received a majority of the traffic, leading to resource exhaustion, while others were underutilized. This imbalance caused high response times and service interruptions for users.</p>

    <p><strong>Resolution:</strong><br>
    The resolution involved adjusting the load balancer configuration to ensure even traffic distribution across all server instances. Specific steps taken included:</p>
    <ol>
        <li>Identifying and correcting the weight settings in the load balancer configuration.</li>
        <li>Redistributing existing traffic manually to balance the load across all servers.</li>
        <li>Implementing and validating configuration changes in a staging environment before applying them to production.</li>
    </ol>

    <h2>Corrective and Preventative Measures</h2>
    <p><strong>Improvements/Fixes:</strong><br>
    To prevent similar issues in the future, the following measures have been identified:</p>
    <ol>
        <li>Enhance Monitoring: Implement more granular monitoring for load balancer performance and traffic distribution.</li>
        <li>Automated Alerts: Set up automated alerts for detecting unusual traffic patterns and load imbalances.</li>
        <li>Load Testing: Conduct regular load testing to validate load balancer configurations under various traffic conditions.</li>
        <li>Documentation and Training: Update internal documentation on load balancer configuration best practices and provide training to relevant team members.</li>
    </ol>

    <p><strong>Task List:</strong></p>
    <ol>
        <li>Patch Nginx Server: Apply the latest patches to the Nginx servers to ensure optimal performance.</li>
        <li>Add Monitoring on Server Memory: Implement monitoring tools to track server memory usage and set up alerts for anomalies.</li>
        <li>Update Load Balancer Configuration: Review and update the load balancer configuration to ensure even traffic distribution.</li>
        <li>Regular Load Testing: Schedule and conduct regular load testing sessions to validate infrastructure resilience.</li>
        <li>Documentation Update: Revise and expand internal documentation regarding load balancer configurations and incident response protocols.</li>
        <li>Team Training: Organize training sessions for the engineering and infrastructure teams on best practices for load balancer management and incident response.</li>
    </ol>

    <div class="image">
        <img src="#" alt="Preventative Measures">
    </div>

    <p>By implementing these corrective and preventative measures, we aim to enhance the resilience and performance of the Naklla application, ensuring a smoother experience for our users and minimizing disruptions in their transportation planning and daily commutes.</p>

    

