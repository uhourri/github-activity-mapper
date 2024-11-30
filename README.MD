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

The **Event-to-Action Mapping** is the first step in transforming raw GitHub events into structured and standardized actions. This process establishes a one-to-one correspondence between GitHub event types and meaningful actions that represent specific contributor operations. The mapping leverages the metadata in each event’s payload to determine the action type and extract relevant details.

#### Mapping Process

##### 1. Raw GitHub Event

A GitHub event represents an action taken by a contributor on the platform. Events are unstructured JSON objects containing various attributes, including the event type, metadata, and payload. For example:

```[EXAMPLE]```

##### 2. Mapping Definition

The mapping file defines rules to translate the raw event into a structured action. These rules specify:
	•	The event type (PullRequestEvent).
	•	Optional payload conditions ("action": "closed" and "merged": true).
	•	Fields to extract and include in the resulting action.

Mapping for the MergePullRequest action is defined as follows:
```[EXAMPLE]```

##### 3. Resulting Action

The raw event is transformed into a structured action. Common fields (e.g., event_id, actor, repository) and action-specific details (e.g., pull_request metadata) are included:

```

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

