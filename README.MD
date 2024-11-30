# GitHub Activity Mapper

This repository contains the **GitHub Activity Mapper**, a tool and associated data mappings for transforming raw GitHub event data into structured actions and high-level activities. This package serves as a replication resource for research purposes, specifically to support analyses of open-source software (OSS) collaboration.

## Repository Structure

```
.
├── LICENSE                     # License information
├── data/                       # Sample datasets for testing and demonstration
│   ├── raw-sample-events.json      # Raw GitHub event data (JSON format)
│   ├── sample-events.json          # Preprocessed sample events (JSON format)
│   ├── sample-actions.jsonl        # Mapped actions (JSON Lines format)
│   ├── sample-activities.jsonl     # High-level activities (JSON Lines format)
├── mapping/                   # Mapping schemas for transformation
│   ├── event-action-mapping.json   # Schema for event-to-action mapping
│   ├── action-activity-mapping.json# Schema for action-to-activity mapping
├── notebooks/                 # Jupyter notebooks for mapping and analysis
│   ├── action-activity-mapping.ipynb  # Notebook for action-to-activity mapping
│   ├── event-action-mapping.ipynb     # Notebook for event-to-action mapping
│   ├── event-preprocessing.ipynb      # Notebook for preprocessing GitHub events
│   ├── numfocus-gh-events-query.ipynb # Notebook for querying NumFocus GitHub events
└── requirements.txt           # Dependencies required to run the code
```

## Getting Started

### Prerequisites

To use this package, ensure you have the following installed:
- Python 3.8 or later
- Jupyter Notebook (for running `.ipynb` files)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/uhourri/github-activity-mapper.git
   cd github-activity-mapper
   ```

2. **Set up a virtual environment:**
   ```bash
   source venv/bin/activate    # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### 1. Querying GitHub Event Data
Extract GitHub event data for NumFocus projects, using the `notebooks/numfocus-gh-events-query.ipynb` notebook.

### 2. Preprocessing GitHub Events
Clean and prepare raw GitHub event data for mapping using the `notebooks/event-preprocessing.ipynb` notebook.

### 3. Mapping GitHub Events to Actions
Use the schema defined in `mapping/event-action-mapping.json` to transform raw GitHub events into granular actions. The process is demonstrated in the `notebooks/event-action-mapping.ipynb` notebook.

The **Event-to-Action Mapping** is the first step in transforming raw GitHub events into structured and standardized actions. This process establishes a one-to-one correspondence between GitHub event types and meaningful actions that represent specific contributor operations. The mapping leverages the metadata in each event’s payload to determine the action type and extract relevant details. with this mapping process :

#### 1. Raw GitHub Event

A GitHub event represents an action taken by a contributor on the platform. Events are unstructured JSON objects containing various attributes, including the event type, metadata, and payload. For example:

```json
{
   "type":"IssuesEvent",
   "public":true,
   "payload":{
      "action":"closed",
      "issue":{
         "url":"https://api.github.com/repos/JuliaLang/julia/issues/48062",
         "repository_url":"https://api.github.com/repos/JuliaLang/julia",
         "labels_url":"https://api.github.com/repos/JuliaLang/julia/issues/48062/labels{/name}",
         "comments_url":"https://api.github.com/repos/JuliaLang/julia/issues/48062/comments",
         "events_url":"https://api.github.com/repos/JuliaLang/julia/issues/48062/events",
         "html_url":"https://github.com/JuliaLang/julia/issues/48062",
         "id":1515182791,
         "node_id":"I_kwDOABkWpM5aT9rH",
         "number":48062,
         "title":"Bad default number of BLAS threads on 1.9?",
         "user":{
            "login":"KristofferC",
            "id":1282691,
            "node_id":"MDQ6VXNlcjEyODI2OTE=",
            "avatar_url":"https://avatars.githubusercontent.com/u/1282691?v=4",
            "url":"https://api.github.com/users/KristofferC",
            "html_url":"https://github.com/KristofferC",
            "followers_url":"https://api.github.com/users/KristofferC/followers",
            "following_url":"https://api.github.com/users/KristofferC/following{/other_user}",
            "gists_url":"https://api.github.com/users/KristofferC/gists{/gist_id}",
            "starred_url":"https://api.github.com/users/KristofferC/starred{/owner}{/repo}",
            "subscriptions_url":"https://api.github.com/users/KristofferC/subscriptions",
            "organizations_url":"https://api.github.com/users/KristofferC/orgs",
            "repos_url":"https://api.github.com/users/KristofferC/repos",
            "events_url":"https://api.github.com/users/KristofferC/events{/privacy}",
            "received_events_url":"https://api.github.com/users/KristofferC/received_events",
            "type":"User",
            "site_admin":false
         },
         "labels":[
            {
               "id":61807486,
               "node_id":"MDU6TGFiZWw2MTgwNzQ4Ng==",
               "url":"https://api.github.com/repos/JuliaLang/julia/labels/linear%20algebra",
               "name":"linear algebra",
               "color":"f2b3db",
               "default":false,
               "description":"Linear algebra"
            }
         ],
         "state":"closed",
         "locked":false,
         "assignee":null,
         "assignees":[
            
         ],
         "milestone":{
            "url":"https://api.github.com/repos/JuliaLang/julia/milestones/44",
            "html_url":"https://github.com/JuliaLang/julia/milestone/44",
            "labels_url":"https://api.github.com/repos/JuliaLang/julia/milestones/44/labels",
            "id":7729972,
            "node_id":"MI_kwDOABkWpM4AdfM0",
            "number":44,
            "title":"1.9",
            "description":"",
            "creator":{
               "login":"vtjnash",
               "id":330950,
               "node_id":"MDQ6VXNlcjMzMDk1MA==",
               "avatar_url":"https://avatars.githubusercontent.com/u/330950?v=4",
               "url":"https://api.github.com/users/vtjnash",
               "html_url":"https://github.com/vtjnash",
               "followers_url":"https://api.github.com/users/vtjnash/followers",
               "following_url":"https://api.github.com/users/vtjnash/following{/other_user}",
               "gists_url":"https://api.github.com/users/vtjnash/gists{/gist_id}",
               "starred_url":"https://api.github.com/users/vtjnash/starred{/owner}{/repo}",
               "subscriptions_url":"https://api.github.com/users/vtjnash/subscriptions",
               "organizations_url":"https://api.github.com/users/vtjnash/orgs",
               "repos_url":"https://api.github.com/users/vtjnash/repos",
               "events_url":"https://api.github.com/users/vtjnash/events{/privacy}",
               "received_events_url":"https://api.github.com/users/vtjnash/received_events",
               "type":"User",
               "site_admin":false
            },
            "open_issues":12,
            "closed_issues":68,
            "state":"open",
            "created_at":"2022-03-02T19:34:37Z",
            "updated_at":"2023-01-01T20:19:58Z",
            "due_on":null,
            "closed_at":null
         },
         "comments":1,
         "created_at":"2022-12-31T18:49:47Z",
         "updated_at":"2023-01-01T20:19:58Z",
         "closed_at":"2023-01-01T20:19:57Z",
         "author_association":"MEMBER",
         "body":"Something looks strange with the number of BLAS threads on 1.9, I think.\n\n```julia\njulia> VERSION\nv\"1.9.0-beta2\"\n\njulia> LinearAlgebra.BLAS.get_num_threads()\n1\n```\n\n```julia\njulia> VERSION\nv\"1.8.4\"\n\njulia> LinearAlgebra.BLAS.get_num_threads()\n8\n```\n\nThis should just be with everything default.\n\ncc @staticfloat",
         "reactions":{
            "url":"https://api.github.com/repos/JuliaLang/julia/issues/48062/reactions",
            "total_count":0,
            "+1":0,
            "-1":0,
            "laugh":0,
            "hooray":0,
            "confused":0,
            "heart":0,
            "rocket":0,
            "eyes":0
         },
         "timeline_url":"https://api.github.com/repos/JuliaLang/julia/issues/48062/timeline",
         "performed_via_github_app":null,
         "state_reason":"completed"
      }
   },
   "repo":{
      "id":1644196,
      "name":"JuliaLang/julia",
      "url":"https://api.github.com/repos/JuliaLang/julia"
   },
   "actor":{
      "id":1282691,
      "login":"KristofferC",
      "avatar_url":"https://avatars.githubusercontent.com/u/1282691?",
      "url":"https://api.github.com/users/KristofferC"
   },
   "org":{
      "id":743164,
      "login":"JuliaLang",
      "avatar_url":"https://avatars.githubusercontent.com/u/743164?",
      "url":"https://api.github.com/orgs/JuliaLang"
   },
   "created_at":1672604398000,
   "id":"26170139709"
}
```

#### 2. Mapping Definition

The mapping file defines rules to translate the raw event into a structured action. These rules specify:
- The event type (IssuesEvent).
- Optional payload conditions ("action": "closed").
- Fields to extract and include in the resulting action.

Mapping for the CloseIssue action is defined as follows:
```json
"CloseIssue":{
   "event":{
      "type":"IssuesEvent",
      "payload":{
         "action":"closed"
      }
   },
   "attributes":{
      "include_common_fields":true,
      "details":{
         "issue":{
            "id":"payload.issue.id",
            "number":"payload.issue.number",
            "title":"payload.issue.title",
            "state":"payload.issue.state",
            "author":{
               "id":"payload.issue.user.id",
               "login":"payload.issue.user.login"
            },
            "labels":[
               {
                  "name":"payload.issue.labels.name",
                  "description":"payload.issue.labels.description"
               }
            ],
            "created_date":"payload.issue.created_at",
            "updated_date":"payload.issue.updated_at",
            "closed_date":"payload.issue.closed_at"
         }
      }
   }
}
```

#### 3. Resulting Action

The raw event is transformed into a structured action. Common fields (e.g., event_id, actor, repository) and action-specific details (e.g., issue metadata) are included:

```json
{
   "action":"CloseIssue",
   "event_id":"26170139709",
   "date":"2023-01-01T20:19:58Z",
   "actor":{
      "id":1282691,
      "login":"KristofferC"
   },
   "repository":{
      "id":1644196,
      "name":"JuliaLang/julia",
      "organisation":"JuliaLang",
      "organisation_id":743164
   },
   "details":{
      "issue":{
         "id":1515182791,
         "number":48062,
         "title":"Bad default number of BLAS threads on 1.9?",
         "state":"closed",
         "author":{
            "id":1282691,
            "login":"KristofferC"
         },
         "labels":[
            {
               "name":"linear algebra",
               "description":"Linear algebra"
            }
         ],
         "created_date":"2022-12-31T18:49:47Z",
         "updated_date":"2023-01-01T20:19:58Z",
         "closed_date":"2023-01-01T20:19:57Z"
      }
   }
}
```
### 4. Mapping Actions to Activities

Use the schema defined in `mapping/action-activity-mapping.json` to aggregate granular actions into high-level activities. This process is demonstrated in the `notebooks/action-activity-mapping.ipynb` notebook.

The **Action-to-Activity Mapping** is the second step in structuring GitHub contributor data. It builds on the Event-to-Action Mapping by grouping related actions into cohesive representations of high-level contributor tasks. Activities encapsulate the broader intent behind individual operations, making them valuable for understanding collaboration and task workflows. with the following mapping precess

#### 1. Actions as Input

Actions, derived from the Event-to-Action Mapping process, serve as the input for this stage. These actions are structured JSON objects containing metadata and detailed attributes. For example:

```json
{
   "action":"CloseIssue",
   "event_id":"26163458157",
   "date":"2023-01-01T00:06:24Z",
   "actor":{
      "id":15819577,
      "login":"mem48"
   },
   "repository":{
      "id":153765492,
      "name":"ropensci/opentripplanner",
      "organisation":"ropensci",
      "organisation_id":1200269
   },
   "details":{
      "issue":{
         "id":755698614,
         "number":78,
         "title":"r5",
         "state":"closed",
         "author":{
            "id":15819577,
            "login":"mem48"
         },
         "labels":[
            {
               "name":"enhancement",
               "description":"New feature or request"
            }
         ],
         "created_date":"2020-12-02T23:54:39Z",
         "updated_date":"2023-01-01T00:06:23Z",
         "closed_date":"2023-01-01T00:06:23Z"
      }
   }
}
```

#### 2. Mapping Definition

The mapping file defines the logic for grouping actions into activities. It specifies:
- The activity type (e.g., CloseIssue).
- Required actions that must occur to form the activity (e.g., CloseIssue).
- Optional actions that may provide additional context (e.g., CreateIssueComment).
- Validation rules to ensure logical consistency (e.g., matching issue numbers between actions).

Mapping for the CloseIssue action is defined as follows:

```json
{
   "name":"CloseIssue",
   "time_window":"3s",
   "actions":[
      {
         "action":"CloseIssue",
         "optional":false,
         "repeat":false
      },
      {
         "action":"CreateIssueComment",
         "optional":true,
         "repeat":false,
         "validate_with":[
            {
               "target_action":"CloseIssue",
               "fields":[
                  {
                     "field":"issue.number",
                     "target_field":"issue.number"
                  }
               ]
            }
         ]
      }
   ]
}
```

#### 3. Resulting Activity

A set of related actions is aggregated into a single activity. Each activity record contains:
- Common fields (e.g., start_date, end_date, actor, repository).
- The list of actions that make up the activity, maintaining traceability to the original operations.

```json
{
   "activity":"CloseIssue",
   "start_date":"2023-01-01T00:06:24Z",
   "end_date":"2023-01-01T00:06:24Z",
   "actor":{
      "id":15819577,
      "login":"mem48"
   },
   "repository":{
      "id":153765492,
      "name":"ropensci/opentripplanner",
      "organisation":"ropensci",
      "organisation_id":1200269
   },
   "actions":[
      {
         "action":"CloseIssue",
         "event_id":"26163458157",
         "date":"2023-01-01T00:06:24Z",
         "details":{
            "issue":{
               "id":755698614,
               "number":78,
               "title":"r5",
               "state":"closed",
               "author":{
                  "id":15819577,
                  "login":"mem48"
               },
               "labels":[
                  {
                     "name":"enhancement",
                     "description":"New feature or request"
                  }
               ],
               "created_date":"2020-12-02T23:54:39Z",
               "updated_date":"2023-01-01T00:06:23Z",
               "closed_date":"2023-01-01T00:06:23Z"
            }
         }
      },
      {
         "action":"CreateIssueComment",
         "event_id":"26163458136",
         "date":"2023-01-01T00:06:24Z",
         "details":{
            "issue":{
               "id":755698614,
               "number":78,
               "title":"r5",
               "state":"closed",
               "author":{
                  "id":15819577,
                  "login":"mem48"
               },
               "labels":[
                  {
                     "name":"enhancement",
                     "description":"New feature or request"
                  }
               ],
               "created_date":"2020-12-02T23:54:39Z",
               "updated_date":"2023-01-01T00:06:23Z",
               "closed_date":"2023-01-01T00:06:23Z"
            },
            "comment":{
               "id":1368298302,
               "position":1
            }
         }
      }
   ]
}
```

This step bridges the gap between granular operations and high-level task representations, enabling nuanced insights into contributor workflows.

## Sample Data

Sample datasets are provided in the `data/` directory:
- `raw-sample-events.json`: Raw GitHub event data.
- `sample-events.json`: Preprocessed GitHub event data.
- `sample-actions.jsonl`: Mapped actions.
- `sample-activities.jsonl`: High-level activities.

## Replication Details

This package supports the replication of methodologies described in the associated research paper. The transformation process involves:

1. **Event-to-Action Mapping**: Converting GitHub events into granular actions.
2. **Action-to-Activity Mapping**: Grouping related actions into high-level activities.

The provided notebooks and sample data demonstrate these steps in a transparent and reproducible manner.

## Contributing

Contributions are welcome! If you identify issues or have suggestions for improvement, please submit an issue or pull request.

## License

This project is licensed under the terms of the [MIT License](LICENSE).

## Contact

For any questions or feedback, please contact [Youness Hourri](mailto:youness.hourri@umons.ac.be).

