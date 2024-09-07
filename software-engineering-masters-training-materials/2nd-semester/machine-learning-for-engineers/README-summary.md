# Machine Learning for Engineers

## Course Overview
This course offers an in-depth introduction to machine learning, tailored for engineers. It focuses on practical applications, model building, evaluation, and deployment. The course includes a mix of theoretical concepts and hands-on programming tasks using popular tools and languages.

## Course Content

### **1. Introduction to Machine Learning**

#### **Supervised vs Unsupervised Learning**
- **Supervised Learning**: Learning from labeled data to predict outcomes for new data. It includes:
  - **Classification**: Predicting categorical labels. Examples: Spam detection, image classification.
  - **Regression**: Predicting continuous values. Examples: House price prediction, temperature forecasting.
  
  **Python Example (Classification with Scikit-learn):**
  ```python
  from sklearn.datasets import load_iris
  from sklearn.model_selection import train_test_split
  from sklearn.linear_model import LogisticRegression
  from sklearn.metrics import accuracy_score
  
  # Load the dataset
  iris = load_iris()
  X = iris.data
  y = iris.target
  
  # Split data into training and testing sets
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
  
  # Initialize and train the model
  model = LogisticRegression(max_iter=200)
  model.fit(X_train, y_train)
  
  # Make predictions and evaluate
  y_pred = model.predict(X_test)
  print("Accuracy:", accuracy_score(y_test, y_pred))
  ```
  
- **Unsupervised Learning**: Learning from unlabeled data to discover patterns. It includes:
  - **Clustering**: Grouping similar data points. Examples: Customer segmentation, market basket analysis.
  - **Dimensionality Reduction**: Reducing the number of features. Examples: PCA for visualization, feature reduction.

  **Python Example (Clustering with K-Means):**
  ```python
  from sklearn.datasets import load_iris
  from sklearn.cluster import KMeans
  import matplotlib.pyplot as plt
  
  # Load the dataset
  iris = load_iris()
  X = iris.data
  
  # Fit K-Means
  kmeans = KMeans(n_clusters=3, random_state=42)
  y_kmeans = kmeans.fit_predict(X)
  
  # Plot the results
  plt.scatter(X[:, 0], X[:, 1], c=y_kmeans, s=50, cmap='viridis')
  plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], c='red', s=200, alpha=0.75)
  plt.title('K-Means Clustering')
  plt.xlabel('Feature 1')
  plt.ylabel('Feature 2')
  plt.show()
  ```

**Practical Exercise:**
- **Implement a Classification Algorithm**: Choose a dataset (e.g., Titanic dataset) and implement a classification model using Scikit-learn.

### **2. Model Building**

#### **Feature Engineering**
- **Feature Extraction**: Creating new features from existing ones to improve model performance. Example: Extracting date features (year, month) from a timestamp.
- **Feature Selection**: Choosing the most relevant features for the model. Example: Using correlation matrices to select features.

  **Python Example (Feature Scaling with StandardScaler):**
  ```python
  from sklearn.preprocessing import StandardScaler
  from sklearn.datasets import load_iris
  from sklearn.model_selection import train_test_split
  from sklearn.linear_model import LogisticRegression
  
  # Load dataset
  iris = load_iris()
  X = iris.data
  y = iris.target
  
  # Feature scaling
  scaler = StandardScaler()
  X_scaled = scaler.fit_transform(X)
  
  # Split data and build model
  X_train, X_test, y_train, y_test = train_test_split(X_scaled, y, test_size=0.3, random_state=42)
  model = LogisticRegression(max_iter=200)
  model.fit(X_train, y_train)
  ```

#### **Model Selection and Tuning**
- **Model Selection**: Choosing the right model for the problem. Example: Decision Trees for interpretability, Neural Networks for complex patterns.
- **Hyperparameter Tuning**: Optimizing model parameters to improve performance. Example: Grid Search for SVM parameters.

  **Python Example (Hyperparameter Tuning with Grid Search):**
  ```python
  from sklearn.model_selection import GridSearchCV
  from sklearn.svm import SVC
  
  # Define parameter grid
  param_grid = {'C': [0.1, 1, 10], 'kernel': ['linear', 'rbf']}
  
  # Grid search
  grid_search = GridSearchCV(SVC(), param_grid, cv=5)
  grid_search.fit(X_train, y_train)
  print("Best parameters:", grid_search.best_params_)
  ```

#### **Cross-Validation and Hyperparameter Optimization**
- **Cross-Validation**: Assess model performance using different subsets of data to ensure robustness.
- **Hyperparameter Optimization**: Techniques like Random Search and Bayesian Optimization to find the best parameters.

**Practical Exercise:**
- **Perform Cross-Validation**: Implement cross-validation for a classification or regression model to evaluate its performance.

### **3. Algorithms and Techniques**

#### **Linear Models**
- **Linear Regression**: Models the relationship between features and target variable.
- **Support Vector Machines (SVM)**: Finds the optimal hyperplane to classify data.

  **Python Example (Linear Regression):**
  ```python
  from sklearn.datasets import load_boston
  from sklearn.linear_model import LinearRegression
  from sklearn.model_selection import train_test_split
  from sklearn.metrics import mean_squared_error
  
  # Load dataset
  boston = load_boston()
  X = boston.data
  y = boston.target
  
  # Split data
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
  
  # Build and evaluate model
  model = LinearRegression()
  model.fit(X_train, y_train)
  y_pred = model.predict(X_test)
  print("Mean Squared Error:", mean_squared_error(y_test, y_pred))
  ```

#### **Decision Trees and Ensemble Methods**
- **Decision Trees**: Split data into subsets based on feature values.
- **Random Forests**: Combine multiple decision trees to improve accuracy.
- **Gradient Boosting**: Sequentially build models to correct previous models' errors.

  **Python Example (Random Forest):**
  ```python
  from sklearn.ensemble import RandomForestClassifier
  from sklearn.datasets import load_iris
  from sklearn.model_selection import train_test_split
  from sklearn.metrics import accuracy_score
  
  # Load dataset
  iris = load_iris()
  X = iris.data
  y = iris.target
  
  # Split data
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
  
  # Build and evaluate model
  model = RandomForestClassifier(n_estimators=100)
  model.fit(X_train, y_train)
  y_pred = model.predict(X_test)
  print("Accuracy:", accuracy_score(y_test, y_pred))
  ```

#### **Neural Networks and Deep Learning**
- **Neural Networks**: Composed of layers of neurons to model complex patterns.
- **Deep Learning**: Advanced neural networks with multiple hidden layers.

  **Python Example (Simple Neural Network with TensorFlow):**
  ```python
  import tensorflow as tf
  from tensorflow.keras.models import Sequential
  from tensorflow.keras.layers import Dense
  from tensorflow.keras.datasets import mnist
  from tensorflow.keras.utils import to_categorical
  
  # Load dataset
  (X_train, y_train), (X_test, y_test) = mnist.load_data()
  X_train = X_train.reshape((60000, 28 * 28)) / 255.0
  X_test = X_test.reshape((10000, 28 * 28)) / 255.0
  y_train = to_categorical(y_train)
  y_test = to_categorical(y_test)
  
  # Build model
  model = Sequential([
      Dense(128, activation='relu', input_shape=(784,)),
      Dense(64, activation='relu'),
      Dense(10, activation='softmax')
  ])
  
  model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
  model.fit(X_train, y_train, epochs=5, batch_size=32, validation_split=0.2)
  print("Test accuracy:", model.evaluate(X_test, y_test)[1])
  ```

**Practical Exercise:**
- **Build and Train a Deep Learning Model**: Use a dataset (e.g., MNIST) to build and train a deep neural network.

### **4. Machine Learning Tools and Frameworks**

#### **Scikit-learn**
- **Tool for Machine Learning**: Provides simple and efficient tools for data mining and data analysis.

  **Python Example (Pipeline with Scikit-learn):**
  ```python
  from sklearn.pipeline import Pipeline
  from sklearn.preprocessing import StandardScaler
  from sklearn.decomposition import PCA
  from sklearn.svm import SVC
  from sklearn.datasets import load_iris
  from sklearn.model_selection import train_test_split
  from sklearn.metrics import accuracy_score
  
  # Load dataset
  iris

 = load_iris()
  X = iris.data
  y = iris.target
  
  # Create pipeline
  pipeline = Pipeline([
      ('scaler', StandardScaler()),
      ('pca', PCA(n_components=2)),
      ('svm', SVC())
  ])
  
  # Split data
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
  
  # Train and evaluate model
  pipeline.fit(X_train, y_train)
  y_pred = pipeline.predict(X_test)
  print("Accuracy:", accuracy_score(y_test, y_pred))
  ```

#### **TensorFlow and PyTorch**
- **TensorFlow**: An open-source library for machine learning and deep learning.
- **PyTorch**: An open-source deep learning platform that provides a seamless path from research to production.

  **Python Example (Simple PyTorch Model):**
  ```python
  import torch
  import torch.nn as nn
  import torch.optim as optim
  from torchvision import datasets, transforms
  
  # Define a simple neural network
  class SimpleNN(nn.Module):
      def __init__(self):
          super(SimpleNN, self).__init__()
          self.fc1 = nn.Linear(28*28, 128)
          self.fc2 = nn.Linear(128, 64)
          self.fc3 = nn.Linear(64, 10)
      
      def forward(self, x):
          x = x.view(-1, 28*28)
          x = torch.relu(self.fc1(x))
          x = torch.relu(self.fc2(x))
          x = self.fc3(x)
          return x
  
  # Load dataset
  transform = transforms.Compose([transforms.ToTensor()])
  trainset = datasets.MNIST(root='./data', train=True, download=True, transform=transform)
  trainloader = torch.utils.data.DataLoader(trainset, batch_size=64, shuffle=True)
  
  # Initialize model, loss function, and optimizer
  model = SimpleNN()
  criterion = nn.CrossEntropyLoss()
  optimizer = optim.Adam(model.parameters())
  
  # Train the model
  for epoch in range(5):
      for images, labels in trainloader:
          optimizer.zero_grad()
          outputs = model(images)
          loss = criterion(outputs, labels)
          loss.backward()
          optimizer.step()
  
  print("Training complete")
  ```

#### **Model Deployment and Monitoring**
- **Deployment**: Deploy models to production using tools like Docker, Kubernetes, or cloud services.
- **Monitoring**: Track model performance and make adjustments as needed using monitoring tools.

  **Python Example (Deploying with Flask):**
  ```python
  from flask import Flask, request, jsonify
  import joblib
  
  app = Flask(__name__)
  model = joblib.load('model.pkl')  # Load pre-trained model
  
  @app.route('/predict', methods=['POST'])
  def predict():
      data = request.json
      features = [data['features']]
      prediction = model.predict(features)
      return jsonify({'prediction': int(prediction[0])})
  
  if __name__ == '__main__':
      app.run(debug=True)
  ```

**Practical Exercise:**
- **Deploy a Machine Learning Model**: Create a REST API to serve a trained model and deploy it using Docker.

### **5. Ethics and Bias in Machine Learning**

#### **Fairness, Accountability, and Transparency**
- **Fairness**: Ensure that models do not disproportionately impact any group. Example: Use fairness metrics to evaluate model decisions.
- **Accountability**: Track and document model decisions to understand and explain predictions.
- **Transparency**: Make the workings and decisions of models understandable to stakeholders.

  **Python Example (Fairness Metrics with Fairness Indicators):**
  ```python
  import fairness_indicators as fi
  from sklearn.metrics import confusion_matrix
  
  # Example data
  y_true = [1, 0, 1, 1, 0, 1, 0]
  y_pred = [1, 0, 1, 0, 0, 1, 1]
  
  # Compute confusion matrix
  cm = confusion_matrix(y_true, y_pred)
  fi.evaluate_fairness(cm)
  ```

#### **Mitigating Bias in Models**
- **Bias Detection**: Analyze datasets and models to identify biases.
- **Bias Mitigation**: Apply techniques to reduce bias, such as re-weighting or adversarial debiasing.

  **Python Example (Mitigating Bias with AI Fairness 360):**
  ```python
  from aif360.datasets import BinaryLabelDataset
  from aif360.metrics import ClassificationMetric
  
  # Load and preprocess dataset
  dataset = BinaryLabelDataset(...)
  
  # Evaluate and mitigate bias
  metric = ClassificationMetric(dataset, ...)
  print("Bias metrics:", metric.bias_metrics)
  ```

**Practical Exercise:**
- **Analyze and Mitigate Bias**: Implement techniques to identify and reduce bias in a machine learning model using fairness libraries.

## **Assessment**

- **Machine Learning Projects**: Implement and evaluate machine learning models using real-world datasets. Include feature engineering, model selection, tuning, and deployment.
- **Midterm Exam**: Assess understanding of machine learning concepts, algorithms, and practical implementations.
- **Final Project**: Complete an end-to-end machine learning pipeline, including data collection, preprocessing, model building, deployment, and monitoring.

## **Resources**

- **"Pattern Recognition and Machine Learning" by Christopher M. Bishop**: Comprehensive textbook covering fundamental and advanced machine learning topics.
- **"Deep Learning" by Ian Goodfellow, Yoshua Bengio, Aaron Courville**: In-depth book on deep learning techniques and principles.
- **Online Tutorials**: For hands-on practice with TensorFlow, PyTorch, and Scikit-learn.
