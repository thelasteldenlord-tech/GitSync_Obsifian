React Reddit Clone

```js


import React, { useState } from 'react';
import { Heart, MessageCircle, Share2, TrendingUp } from 'lucide-react';

export default function RedditClone() {
  const [posts, setPosts] = useState([
    {
      id: 1,
      author: "TechEnthusiast",
      content: "Just discovered this amazing new web framework! The developer experience is incredible and the performance is blazing fast. Anyone else tried it?",
      likes: 42,
      comments: 8,
      timeAgo: "2h ago",
      liked: false
    },
    {
      id: 2,
      author: "NatureLover",
      content: "Went hiking today and saw the most beautiful sunset. Sometimes you just need to disconnect from technology and reconnect with nature. 🌅",
      likes: 127,
      comments: 23,
      timeAgo: "4h ago",
      liked: false
    },
    {
      id: 3,
      author: "CodeWizard",
      content: "Pro tip: Always write your code like the person who ends up maintaining it is a violent psychopath who knows where you live. Clean code saves lives! 😄",
      likes: 89,
      comments: 15,
      timeAgo: "6h ago",
      liked: false
    }
  ]);

  const [newPost, setNewPost] = useState({ author: '', content: '' });
  const [showForm, setShowForm] = useState(false);

  const handleSubmit = () => {
    if (newPost.author.trim() && newPost.content.trim()) {
      const post = {
        id: Date.now(),
        author: newPost.author,
        content: newPost.content,
        likes: 0,
        comments: 0,
        timeAgo: 'now',
        liked: false
      };
      setPosts([post, ...posts]);
      setNewPost({ author: '', content: '' });
      setShowForm(false);
    }
  };

  const toggleLike = (postId) => {
    setPosts(posts.map(post => 
      post.id === postId 
        ? { 
            ...post, 
            liked: !post.liked,
            likes: post.liked ? post.likes - 1 : post.likes + 1
          }
        : post
    ));
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900">
      {/* Header */}
      <header className="bg-black/20 backdrop-blur-xl border-b border-purple-500/20 sticky top-0 z-50">
        <div className="max-w-4xl mx-auto px-4 py-4">
          <div className="flex items-center justify-between">
            <div className="flex items-center space-x-3">
              <div className="w-8 h-8 bg-gradient-to-r from-purple-400 to-pink-400 rounded-full flex items-center justify-center">
                <TrendingUp className="w-5 h-5 text-white" />
              </div>
              <h1 className="text-2xl font-bold bg-gradient-to-r from-purple-400 to-pink-400 bg-clip-text text-transparent">
                SocialFeed
              </h1>
            </div>
            <button
              onClick={() => setShowForm(!showForm)}
              className="px-6 py-2 bg-gradient-to-r from-purple-500 to-pink-500 text-white rounded-full font-medium hover:from-purple-600 hover:to-pink-600 transform hover:scale-105 transition-all duration-200 shadow-lg"
            >
              {showForm ? 'Cancel' : 'Create Post'}
            </button>
          </div>
        </div>
      </header>

      <div className="max-w-4xl mx-auto px-4 py-6">
        {/* Create Post Form */}
        {showForm && (
          <div className="bg-black/20 backdrop-blur-xl rounded-2xl border border-purple-500/20 p-6 mb-6 shadow-2xl">
            <h2 className="text-xl font-semibold text-white mb-4">Share your thoughts</h2>
            <div className="space-y-4">
              <div>
                <input
                  type="text"
                  placeholder="Your name"
                  value={newPost.author}
                  onChange={(e) => setNewPost({...newPost, author: e.target.value})}
                  className="w-full px-4 py-3 bg-white/10 border border-purple-500/30 rounded-xl text-white placeholder-gray-300 focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent transition-all duration-200"
                />
              </div>
              <div>
                <textarea
                  placeholder="What's on your mind?"
                  value={newPost.content}
                  onChange={(e) => setNewPost({...newPost, content: e.target.value})}
                  rows="4"
                  className="w-full px-4 py-3 bg-white/10 border border-purple-500/30 rounded-xl text-white placeholder-gray-300 focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent resize-none transition-all duration-200"
                />
              </div>
              <div className="flex justify-end space-x-3">
                <button
                  onClick={() => setShowForm(false)}
                  className="px-6 py-2 text-gray-300 hover:text-white transition-colors duration-200"
                >
                  Cancel
                </button>
                <button
                  onClick={handleSubmit}
                  className="px-6 py-2 bg-gradient-to-r from-purple-500 to-pink-500 text-white rounded-xl font-medium hover:from-purple-600 hover:to-pink-600 transform hover:scale-105 transition-all duration-200 shadow-lg"
                >
                  Post
                </button>
              </div>
            </div>
          </div>
        )}

        {/* Posts Feed */}
        <div className="space-y-4">
          {posts.map((post) => (
            <div
              key={post.id}
              className="bg-black/20 backdrop-blur-xl rounded-2xl border border-purple-500/20 p-6 hover:border-purple-400/40 transition-all duration-300 shadow-xl hover:shadow-2xl transform hover:-translate-y-1"
            >
              {/* Post Header */}
              <div className="flex items-center justify-between mb-4">
                <div className="flex items-center space-x-3">
                  <div className="w-10 h-10 bg-gradient-to-r from-purple-400 to-pink-400 rounded-full flex items-center justify-center">
                    <span className="text-white font-bold text-sm">
                      {post.author[0].toUpperCase()}
                    </span>
                  </div>
                  <div>
                    <h3 className="text-white font-medium">{post.author}</h3>
                    <p className="text-gray-400 text-sm">{post.timeAgo}</p>
                  </div>
                </div>
              </div>

              {/* Post Content */}
              <div className="mb-4">
                <p className="text-gray-200 leading-relaxed">{post.content}</p>
              </div>

              {/* Post Actions */}
              <div className="flex items-center space-x-6 pt-4 border-t border-purple-500/20">
                <button
                  onClick={() => toggleLike(post.id)}
                  className={`flex items-center space-x-2 px-3 py-2 rounded-lg transition-all duration-200 ${
                    post.liked
                      ? 'text-pink-400 bg-pink-400/10'
                      : 'text-gray-400 hover:text-pink-400 hover:bg-pink-400/10'
                  }`}
                >
                  <Heart className={`w-5 h-5 ${post.liked ? 'fill-current' : ''}`} />
                  <span className="font-medium">{post.likes}</span>
                </button>
                
                <button className="flex items-center space-x-2 px-3 py-2 rounded-lg text-gray-400 hover:text-blue-400 hover:bg-blue-400/10 transition-all duration-200">
                  <MessageCircle className="w-5 h-5" />
                  <span className="font-medium">{post.comments}</span>
                </button>
                
                <button className="flex items-center space-x-2 px-3 py-2 rounded-lg text-gray-400 hover:text-green-400 hover:bg-green-400/10 transition-all duration-200">
                  <Share2 className="w-5 h-5" />
                  <span className="font-medium">Share</span>
                </button>
              </div>
            </div>
          ))}
        </div>

        {/* Footer */}
        <div className="text-center mt-12 py-8">
          <p className="text-gray-400">
            Share your thoughts with the world ✨
          </p>
        </div>
      </div>
    </div>
  );
}