**Subject: Interview Questions and Answers**

**Dear Team ArcTech,**

I sincerely apologize for the delayed submission of my responses. I understand the importance of meeting deadlines and truly regret any inconvenience this may have caused. I appreciate your consideration and hope my answers demonstrate my competence. Due to certain reasons, I was unable to respond earlier. Please consider my response.

---

### **1) Example of an Async/Await-Based Function to Fetch Data from the JSONPlaceholder API**

Here is an example of an async/await function for fetching data:

```javascript
async function fetchData() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}

fetchData().then((data) => console.log(data));
```

**Explanation:**

- The `fetch` API is used to retrieve data from [JSONPlaceholder](https://jsonplaceholder.typicode.com/).
- Since API calls are asynchronous, `async/await` is used to manage the asynchronous behavior.
- The `.json()` method is applied to convert the raw response into JSON format.
- Since `fetch` returns a promise, we use `.then(data => console.log(data));` to log the data if the promise resolves successfully.

---

### **2) Displaying Data in an MUI Table**

#### **a) Create a Redux Slice (slice.js):**

```javascript
import { createSlice } from "@reduxjs/toolkit";

const dataSlice = createSlice({
  name: "data",
  initialState: {
    value: [],
  },
  reducers: {
    setData: (state, action) => {
      state.value = action.payload;
    },
  },
});

export const { setData } = dataSlice.actions;
export default dataSlice.reducer;
```

#### **b) Create a Redux Store (store.js):**

```javascript
import { configureStore } from "@reduxjs/toolkit";
import dataSlice from "./slice";

export const store = configureStore({
  reducer: dataSlice,
});
```

#### **c) Create DataTable Component (DataTable.jsx):**

```javascript
import React, { useEffect } from "react";
import { useDispatch, useSelector } from "react-redux";
import { setData } from "../redux/slice";
import {
  Table,
  TableBody,
  TableCell,
  TableContainer,
  TableHead,
  TableRow,
  Paper,
  useMediaQuery,
} from "@mui/material";

function DataTable() {
  const isMobile = useMediaQuery("(max-width:600px)");
  const data = useSelector((state) => state.value);
  const dispatch = useDispatch();

  const fetchData = async () => {
    try {
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/users"
      );
      const data = await response.json();
      dispatch(setData(data));
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  };

  useEffect(() => {
    fetchData();
  }, []);

  return (
    <div className="p-4">
      <TableContainer
        component={Paper}
        sx={{ width: isMobile ? "100%" : "50%", margin: "auto" }}
      >
        <Table>
          <TableHead>
            <TableRow>
              <TableCell>ID</TableCell>
              <TableCell>Name</TableCell>
              <TableCell>Username</TableCell>
            </TableRow>
          </TableHead>
          <TableBody>
            {data.map((item) => (
              <TableRow key={item.id}>
                <TableCell>{item.id}</TableCell>
                <TableCell>{item.name}</TableCell>
                <TableCell>{item.username}</TableCell>
              </TableRow>
            ))}
          </TableBody>
        </Table>
      </TableContainer>
    </div>
  );
}

export default DataTable;
```

#### **d) Update `main.jsx`:**

```javascript
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App.jsx";
import { Provider } from "react-redux";
import { store } from "./redux/store.js";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </StrictMode>
);
```

#### **e) Add DataTable Component in `App.jsx`:**

```javascript
import DataTable from "./components/DataTable";

function App() {
  return (
    <div>
      <DataTable />
    </div>
  );
}

export default App;
```

---

### **3) Passing the Redux Store to a React JS Page**

To pass the Redux store to a React page, follow these steps:

#### **a) Create a Redux Slice:**

```javascript
import { createSlice } from "@reduxjs/toolkit";

const dataSlice = createSlice({
  name: "data",
  initialState: {
    value: [],
  },
  reducers: {
    setData: (state, action) => {
      state.value = action.payload;
    },
  },
});

export const { setData } = dataSlice.actions;
export default dataSlice.reducer;
```

#### **b) Create a Redux Store:**

Add redux slice to redux store

```javascript
import { configureStore } from "@reduxjs/toolkit";
import dataSlice from "./slice";

export const store = configureStore({
  reducer: dataSlice,
});
```

#### **c) Wrap the App with the Redux Provider:**

In `main.jsx`:

```javascript
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App.jsx";
import { Provider } from "react-redux";
import { store } from "./redux/store.js";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </StrictMode>
);
```

#### **d) Access the Store in a Component:**

components access the store via useSelector and useDispatch hooks.

```javascript
import { useDispatch, useSelector } from "react-redux";
import { setData } from "../redux/slice";
import { useEffect } from "react";
import { useMediaQuery } from "@mui/material";

function DataTable() {
  const isMobile = useMediaQuery("(max-width:600px)");
  const data = useSelector((state) => state.value);
  const dispatch = useDispatch();

  const fetchData = async () => {
    try {
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/users"
      );
      const data = await response.json();
      dispatch(setData(data));
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  };

  useEffect(() => {
    fetchData();
  }, []);
}
```

---

### **4) React JS Table as a Mind Map**

**Sorry but I didn't actually understood the 4th question what exactly you are asking.**

But if you are asking how i will summarize it the whole code above as mindmap this is my answer

Display Table in React JS
├── Data Fetching
│ ├── Fetch API
│ ├── Async/Await
│ ├── Loading State
│ └── Error Handling
├── UI Components
│ ├── Table Structure
│ ├── Headers and Rows
│ └── Responsive Design
├── State Management
│ ├── React State
│ ├── Redux Store
│ └── Connecting Components
├── Optimization
│ ├── Pagination
│ ├── Memoization
│ └── Code Splitting

**I appreciate your time and consideration in reviewing my responses. Looking forward to your feedback.**

**Best regards,**
Nileshkumar Yadav
