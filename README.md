# Real-time Election Voting System 🗳️

This repository contains the code for a real-time election voting system developed to address concerns about election integrity and transparency. In response to allegations of a rigged voting system favoring the ruling party BJP in India, this system was designed to ensure a fair and transparent electoral process.

## System Architecture 🏗️
![system_architecture.jpg](images%2Fsystem_architecture.jpg)

## System Flow 🔄
![system_flow.jpg](images%2Fsystem_flow.jpg)

## System Components 🧩
- **main.py**: Creates the required tables in Postgres (`candidates`, `voters`, and `votes`), creates the Kafka topic, and replicates the `votes` table in the Kafka topic. It also contains the logic to consume votes from the Kafka topic and produce data to `voters_topic` on Kafka.
- **voting.py**: Contains the logic to consume votes from the Kafka topic (`voters_topic`), generate voting data, and produce data to `votes_topic` on Kafka.
- **spark-streaming.py**: Contains the logic to consume votes from the Kafka topic (`votes_topic`), enrich the data from Postgres, aggregate the votes, and produce data to specific topics on Kafka.
- **streamlit-app.py**: Contains the logic to consume the aggregated voting data from the Kafka topic and Postgres, displaying the voting data in real-time using Streamlit.

## Setting Up the System 🛠️

Follow these steps to set up the real-time election voting system:

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/realtime-election-voting-system.git
   cd realtime-election-voting-system

This Docker Compose file allows you to easily spin up Zookkeeper, Kafka and Postgres application in Docker containers. 

### Prerequisites
- Python 3.9 or above installed on your machine
- Docker Compose installed on your machine
- Docker installed on your machine


### Steps to Run
1. Clone this repository.
2. Navigate to the root containing the Docker Compose file.
3. Run the following command:

```bash
docker-compose up -d
```
This command will start Zookeeper, Kafka and Postgres containers in detached mode (`-d` flag). Kafka will be accessible at `localhost:9092` and Postgres at `localhost:5432`.

##### Additional Configuration
If you need to modify Zookeeper configurations or change the exposed port, you can update the `docker-compose.yml` file according to your requirements.

### Running the App
1. Install the required Python packages using the following command:

```bash
pip install -r requirements.txt
```

2. Creating the required tables on Postgres and generating voter information on Kafka topic:

```bash
python main.py
```

3. Consuming the voter information from Kafka topic, generating voting data and producing data to Kafka topic:

```bash
python voting.py
```

4. Consuming the voting data from Kafka topic, enriching the data from Postgres and producing data to specific topics on Kafka:

```bash
python spark-streaming.py
```

5. Running the Streamlit app:

```bash
streamlit run streamlit-app.py
```

## Screenshots

### Voters
![voters.png](images%2Fvoters.png)

### Voting
![voting.png](images%2Fvoting.png)

