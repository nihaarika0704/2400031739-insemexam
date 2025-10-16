import React, { useState } from "react";

const SortableTable = () => {
  // Step 1: Employee data array
  const employees = [
    { name: "Alice Johnson", department: "Engineering", salary: 80000 },
    { name: "Bob Smith", department: "Sales", salary: 65000 },
    { name: "Charlie Lee", department: "HR", salary: 72000 },
    { name: "Diana Adams", department: "Marketing", salary: 70000 },
    { name: "Ethan Brown", department: "Engineering", salary: 90000 },
  ];

  // Step 2: State for sorted data & sorting configuration
  const [sortedData, setSortedData] = useState(employees);
  const [sortConfig, setSortConfig] = useState({ key: null, direction: "asc" });

  // Step 3: Sorting function
  const handleSort = (key) => {
    let direction = "asc";

    // Toggle direction when clicking the same header twice
    if (sortConfig.key === key && sortConfig.direction === "asc") {
      direction = "desc";
    }

    const sorted = [...sortedData].sort((a, b) => {
      if (a[key] < b[key]) return direction === "asc" ? -1 : 1;
      if (a[key] > b[key]) return direction === "asc" ? 1 : -1;
      return 0;
    });

    setSortedData(sorted);
    setSortConfig({ key, direction });
  };

  // Step 4: Render the table
  return (
    <div className="p-6 flex flex-col items-center">
      <h2 className="text-2xl font-bold mb-4 text-gray-800">
        🧑‍💼 Employee Table
      </h2>

      <table className="min-w-full border border-gray-300 rounded-lg shadow-md">
        <thead>
          <tr className="bg-gray-100">
            <th
              onClick={() => handleSort("name")}
              className="p-3 border cursor-pointer hover:bg-gray-200"
            >
              Name{" "}
              {sortConfig.key === "name" &&
                (sortConfig.direction === "asc" ? "↑" : "↓")}
            </th>
            <th
              onClick={() => handleSort("department")}
              className="p-3 border cursor-pointer hover:bg-gray-200"
            >
              Department{" "}
              {sortConfig.key === "department" &&
                (sortConfig.direction === "asc" ? "↑" : "↓")}
            </th>
            <th
              onClick={() => handleSort("salary")}
              className="p-3 border cursor-pointer hover:bg-gray-200"
            >
              Salary{" "}
              {sortConfig.key === "salary" &&
                (sortConfig.direction === "asc" ? "↑" : "↓")}
            </th>
          </tr>
        </thead>

        <tbody>
          {sortedData.map((emp, index) => (
            <tr
              key={index}
              className={`text-center ${
                index % 2 === 0 ? "bg-white" : "bg-gray-50"
              } hover:bg-blue-50 transition-colors`}
            >
              <td className="p-3 border">{emp.name}</td>
              <td className="p-3 border">{emp.department}</td>
              <td className="p-3 border">${emp.salary.toLocaleString()}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default SortableTable;

           
