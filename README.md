# React Internship Task

## 🚀 **Overview**
This project demonstrates basic React.js concepts, including:
- **Async/Await** for API requests
- **Redux Toolkit** for state management
- **Material-UI (MUI)** for table design
- **Responsive Design** using CSS styles

---

## 🔗 **1. API Integration**
- Data is fetched from the **JSONPlaceholder API**:  
  `https://jsonplaceholder.typicode.com/users`
- Uses `fetch` with `async/await` for smooth asynchronous requests.

```javascript
const fetchData = async (dispatch) => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    const data = await response.json();
    dispatch(setData(data));
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};
```

- **Why pass `dispatch`?**
  - To **update the Redux store** after data is fetched.
  - `dispatch(setData(data))` triggers the `setData` reducer to store data globally.

---

## 📦 **2. Redux State Management**

### ✅ **Slice Setup:**
```javascript
const dataSlice = createSlice({
  name: 'data',
  initialState: { value: [] },
  reducers: {
    setData: (state, action) => {
      state.value = action.payload;
    },
  },
});
```

### 🚀 **Store Configuration:**
```javascript
const store = configureStore({ reducer: dataSlice.reducer });
```

### 📊 **Connecting Redux with React:**
- `Provider` wraps the entire app to give Redux access.
- `useSelector` reads data from the store.
- `useDispatch` dispatches actions.

```javascript
const data = useSelector((state) => state.value);
const dispatch = useDispatch();
```

---

## 📋 **3. MUI Table for Displaying Data**
- Data is displayed in a **Material-UI table**.
- Responsive design: 
  - **50% width** on laptop screens
  - **100% width** on mobile screens

```javascript
<TableContainer component={Paper} style={{ width: '100%', maxWidth: '50%', margin: 'auto' }}>
  <Table>
    <TableHead>
      <TableRow>
        <TableCell>ID</TableCell>
        <TableCell>Name</TableCell>
        <TableCell>Username</TableCell>
      </TableRow>
    </TableHead>
    <TableBody>
      {data.map((user) => (
        <TableRow key={user.id}>
          <TableCell>{user.id}</TableCell>
          <TableCell>{user.name}</TableCell>
          <TableCell>{user.username}</TableCell>
        </TableRow>
      ))}
    </TableBody>
  </Table>
</TableContainer>
```


## ⚡ **Technologies Used**
- React.js
- Redux Toolkit
- Material-UI
- Fetch API

---

## 🙏 **Credits**
Prepared for the **ArcTech Internship** selection process.

