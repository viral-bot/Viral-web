import React, { useState, useEffect } from 'react';
import { BrowserRouter, Route, Routes, Link } from 'react-router-dom';

const App = () => {
  const [videos, setVideos] = useState([
    { id: 1, title: 'Video 1', description: 'This is video 1', views: 100, likes: 10 },
    { id: 2, title: 'Video 2', description: 'This is video 2', views: 200, likes: 20 },
    { id: 3, title: 'Video 3', description: 'This is video 3', views: 300, likes: 30 },
  ]);

  const [selectedVideo, setSelectedVideo] = useState(null);

  useEffect(() => {
    setSelectedVideo(videos[0]);
  }, [videos]);

  return (
    <BrowserRouter>
      <div className="flex flex-col h-screen">
        <header className="bg-gray-800 text-white p-4">
          <nav className="flex justify-between">
            <Link to="/" className="text-lg font-bold">
              YouTube Clone
            </Link>
            <ul className="flex items-center space-x-4">
              <li>
                <Link to="/videos">Videos</Link>
              </li>
              <li>
                <Link to="/upload">Upload</Link>
              </li>
            </ul>
          </nav>
        </header>
        <main className="flex-1">
          <Routes>
            <Route
              path="/"
              element={
                <Home videos={videos} setSelectedVideo={setSelectedVideo} />
              }
            />
            <Route
              path="/videos"
              element={
                <Videos videos={videos} setSelectedVideo={setSelectedVideo} />
              }
            />
            <Route path="/upload" element={<Upload />} />
            <Route
              path="/videos/:id"
              element={
                <VideoPlayer video={selectedVideo} videos={videos} />
              }
            />
          </Routes>
        </main>
      </div>
    </BrowserRouter>
  );
};

const Home = ({ videos, setSelectedVideo }) => {
  return (
    <div className="p-4">
      <h1 className="text-lg font-bold mb-4">Recommended Videos</h1>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        {videos.map((video) => (
          <VideoCard
            key={video.id}
            video={video}
            setSelectedVideo={setSelectedVideo}
          />
        ))}
      </div>
    </div>
  );
};

const Videos = ({ videos, setSelectedVideo }) => {
  return (
    <div className="p-4">
      <h1 className="text-lg font-bold mb-4">All Videos</h1>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        {videos.map((video) => (
          <VideoCard
            key={video.id}
            video={video}
            setSelectedVideo={setSelectedVideo}
          />
        ))}
      </div>
    </div>
  );
};

const VideoCard = ({ video, setSelectedVideo }) => {
  return (
    <div className="bg-white rounded-lg shadow-md p-4">
      <div className="bg-gray-200 border-2 border-dashed rounded-xl w-16 h-16 mb-4" />
      <h2 className="text-lg font-bold mb-2">{video.title}</h2>
      <p className="text-gray-600 mb-4">{video.description}</p>
      <div className="flex justify-between">
        <span className="text-gray-600">{video.views} views</span>
        <span className="text-gray-600">{video.likes} likes</span>
      </div>
      <button
        className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mt-4"
        onClick={() => setSelectedVideo(video)}
      >
        Watch Now
      </button>
    </div>
  );
};

const VideoPlayer = ({ video, videos }) => {
  return (
    <div className="p-4">
      <h1 className="text-lg font-bold mb-4">{video.title}</h1>
      <div className="bg-gray-200 border-2 border-dashed rounded-xl w-full h-64 mb-4" />
      <p className="text-gray-600 mb-4">{video.description}</p>
      <div className="flex justify-between">
        <span className="text-gray-600">{video.views} views</span>
        <span className="text-gray-600">{video.likes} likes</span>
      </div>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mt-4">
        {videos
          .filter((v) => v.id !== video.id)
          .map((v) => (
            <VideoCard key={v.id} video={v} />
          ))}
      </div>
    </div>
  );
};

const Upload = () => {
  return (
    <div className="p-4">
      <h1 className="text-lg font-bold mb-4">Upload Video</h1>
      <form>
        <input
          type="text"
          className="block w-full p-2 mb-4 border border-gray-400 rounded-lg"
          placeholder="Title"
        />
        <textarea
          className="block w-full p-2 mb-4 border border-gray-400 rounded-lg"
          placeholder="Description"
        />
        <button
          className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
          type="submit"
        >
          Upload
        </button>
      </form>
    </div>
  );
};
import React, { useState, useEffect } from 'react';
import { BrowserRouter, Route, Routes, Link } from 'react-router-dom';

const App = () => {
  const [videos, setVideos] = useState([
    { id: 1, title: 'Video 1', description: 'This is video 1', views: 100, likes: 10 },
    { id: 2, title: 'Video 2', description: 'This is video 2', views: 200, likes: 20 },
    { id: 3, title: 'Video 3', description: 'This is video 3', views: 300, likes: 30 },
  ]);

  const [selectedVideo, setSelectedVideo] = useState(null);

  useEffect(() => {
    setSelectedVideo(videos[0]);
  }, [videos]);

  return (
    <BrowserRouter>
      <div className="flex flex-col h-screen">
        <header className="bg-gray-800 text-white p-4">
          <nav className="flex justify-between">
            <Link to="/" className="text-lg font-bold">
              YouTube Clone
            </Link>
            <ul className="flex items-center space-x-4">
              <li>
                <Link to="/videos">Videos</Link>
              </li>
              <li>
                <Link to="/upload">Upload</Link>
              </li>
            </ul>
          </nav>
        </header>
        <main className="flex-1">
          <Routes>
            <Route
              path="/"
              element={
                <Home videos={videos} setSelectedVideo={setSelectedVideo} />
              }
            />
            <Route
              path="/videos"
              element={
                <Videos videos={videos} setSelectedVideo={setSelectedVideo} />
              }
            />
            <Route path="/upload" element={<Upload />} />
            <Route
              path="/videos/:id"
              element={
                <VideoPlayer video={selectedVideo} videos={videos} />
              }
            />
          </Routes>
        </main>
      </div>
    </BrowserRouter>
  );
};

const Home = ({ videos, setSelectedVideo }) => {
  return (
    <div className="p-4">
      <h1 className="text-lg font-bold mb-4">Recommended Videos</h1>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        {videos.map((video) => (
          <VideoCard
            key={video.id}
            video={video}
            setSelectedVideo={setSelectedVideo}
          />
        ))}
      </div>
    </div>
  );
};

const Videos = ({ videos, setSelectedVideo }) => {
  return (
    <div className="p-4">
      <h1 className="text-lg font-bold mb-4">All Videos</h1>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        {videos.map((video) => (
          <VideoCard
            key={video.id}
            video={video}
            setSelectedVideo={setSelectedVideo}
          />
        ))}
      </div>
    </div>
  );
};

const VideoCard = ({ video, setSelectedVideo }) => {
  return (
    <div className="bg-white rounded-lg shadow-md p-4">
      <div className="bg-gray-200 border-2 border-dashed rounded-xl w-16 h-16 mb-4" />
      <h2 className="text-lg font-bold mb-2">{video.title}</h2>
      <p className="text-gray-600 mb-4">{video.description}</p>
      <div className="flex justify-between">
        <span className="text-gray-600">{video.views} views</span>
        <span className="text-gray-600">{video.likes} likes</span>
      </div>
      <button
        className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mt-4"
        onClick={() => setSelectedVideo(video)}
      >
        Watch Now
      </button>
    </div>
  );
};

const VideoPlayer = ({ video, videos }) => {
  return (
    <div className="p-4">
      <h1 className="text-lg font-bold mb-4">{video.title}</h1>
      <div className="bg-gray-200 border-2 border-dashed rounded-xl w-full h-64 mb-4" />
      <p className="text-gray-600 mb-4">{video.description}</p>
      <div className="flex justify-between">
        <span className="text-gray-600">{video.views} views</span>
        <span className="text-gray-600">{video.likes} likes</span>
      </div>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mt-4">
        {videos
          .filter((v) => v.id !== video.id)
          .map((v) => (
            <VideoCard key={v.id} video={v} />
          ))}
      </div>
    </div>
  );
};

const Upload = () => {
  return (
    <div className="p-4">
      <h1 className="text-lg font-bold mb-4">Upload Video</h1>
      <form>
        <input
          type="text"
          className="block w-full p-2 mb-4 border border-gray-400 rounded-lg"
          placeholder="Title"
        />
        <textarea
          className="block w-full p-2 mb-4 border border-gray-400 rounded-lg"
          placeholder="Description"
        />
        <button
          className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
          type="submit"
        >
          Upload
        </button>
      </form>
    </div>
  );
};
