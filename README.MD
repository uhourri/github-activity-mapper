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

### 4. Mapping Actions to Activities
Aggregate related actions into high-level activities using the schema in `mapping/action-activity-mapping.json`. Refer to the `notebooks/action-activity-mapping.ipynb` notebook for an implementation example.


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

