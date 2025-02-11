# Calculator App

![Screenshot 2025-02-11 at 11 05 40 AM](https://github.com/user-attachments/assets/b99ad8da-a204-447b-a615-53e7208bceca)

**Logic:**

- Manage Input state, Display result of calculation using eval function in the input box.
- For setting values of button into input tag attach id for each button and fire event on their parent div tag.
- So, on the basis of e.target.id will get the value of each button.

App.jsx

```jsx
import { useState } from "react";

const App = () => {
  const [input, setInput] = useState("");

  const arr = [
    "1", "2", "3", "4", "5",
    "6", "7", "8", "9", "0",
    "+", "-", "/", "*", "=",
    "C", ".",
  ];

  const handleClick = (e) => {
    const id = e.target.id;

    if (e.target.id === "C") {
      setInput("");
    } else if (e.target.id === "=") {
      // Calculate result
      handleSubmit();
    } else {
      setInput((prev) => prev + id);
    }
  };

  const handleSubmit = (e) => {
    e?.preventDefault();

    try {
      const ans = eval(input);
      setInput(ans);
    } catch (err) {
      alert("Invalid Inputs");
    }
  };

  return (
    <div className="container mx-auto">
      <h1 className="my-4 text-3xl text-center">Calculator App</h1>

      <div className="my-4">
        <div>
          <form onSubmit={handleSubmit}>
            <input
              className="w-full border border-slate-200 rounded p-2"
              type="text"
              value={input}
              onChange={(e) => setInput(e.target.value)}
            />
          </form>
        </div>

        <div
          className="mt-5 h-[50vh] grid grid-cols-3 gap-1"
          onClick={handleClick}
        >
          {arr.map((item, idx) => (
            <button
              className="bg-orange-400 text-white font-bold rounded hover:cursor-pointer"
              id={item}
              key={idx}
            >
              {item}
            </button>
          ))}
        </div>
      </div>
    </div>
  );
};

export default App;

```
