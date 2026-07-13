# React Interview Programs (Practice Collection)

# 19. AutoSearch with debounce

``` javascript

import React, { useState, useEffect, useRef } from 'react';
import './style.css';

export default function App() {
 const [search, setSearch] = useState('');
 const [data, setData] = useState([]);
 const [searchResult, setSearchResult] = useState([]);
 const cache = useRef({});

 const handleSearch = (e) => {
   setSearch(e.target.value);
 };


 useEffect(() => {
   try {
     fetch('https://jsonplaceholder.typicode.com/posts/1/comments')
       .then((response) => response.json())
       .then((data) => {
         setData(data);
         setSearchResult(data);
       });
   } catch (e) {
     console.log(e);
   }
 }, []);


 useEffect(() => {
   const timer = setTimeout(() => {
     if (!search.trim()) {
       setSearchResult(data);
       return;
     }
      if (cache.current[search]) {
       setSearchResult(cache.current[search]);
       return;
     }
      const filtered = data.filter((item) =>
       item.name.toLowerCase().includes(search.toLowerCase())
     );
      cache.current[search] = filtered;
      setSearchResult(filtered);
   }, 500);
    return () => clearTimeout(timer);
 }, [search, data]);


  return (
   <div className="container">
     <div className="autocomplete">
       <h2 className="title">Autocomplete Search</h2>
       <input
         className="searchInput"
         type="text"
         placeholder="Search names..."
         onChange={handleSearch}
         value={search}
       />
       <div className="resultContainer">
         {searchResult.length ? (
           <ul className="resultList">
             {searchResult.map((item) => (
               <li className="resultItem" key={item.id}>
                 {item.name}
               </li>
             ))}
           </ul>
         ) : (
           <div className="noResult">No Result Found</div>
         )}
       </div>
     </div>
   </div>
 );
}
```
