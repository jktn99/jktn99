- import React, { useState, useEffect } from 'react';

const InfiniteScroll = () => {
  const [items, setItems] = useState([]);
  const [page, setPage] = useState(1);

  const fetchMoreData = () => {
    // Simulate fetching more data from an API
    const newData = [...items, ...newItems];
    setItems(newData);
    setPage(page + 1);
  };

  useEffect(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        if (entries[0].isIntersecting) {
          fetchMoreData();
        }
      },
      { threshold: 1 }
    );

    observer.observe(document.querySelector('#observer'));

    return () => observer.disconnect();
  }, [page]);

  return (
    <div>
      {items.map((item, index) => (
        <div key={index}>{item}</div>
      ))}
      <div id="observer" style={{ height: '10px' }}></div>
    </div>
  );
};

export default InfiniteScroll;

