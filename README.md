### 1. Optimization blade @foreach
    @if($posts->count())
        @foreach($posts as $item)
            {{$item->name}}
        @endforeach
    @else
        Nothing found
    @endif

### @forelse
    
    @forelse($posts as $item)
        {{$item->name}}
    @empty
        Nothing found
    @endforelse

### @each

 Add partial files

#### empty-posts.blade.php
    <p>Nothing found</p>
#### post.blade.php
    <p>{{$post->name}}</p>
#### @each
    @each('partial.post',$posts,'post','partial.empty-posts')

### 2. Reminder lazy-load "with()" (Laravel - 8.43)
Maybe in Laravel 9 it will be added to the config
#### AppServiceProvider.php

    public function boot()
    {
        Model::preventLazyLoading(!app()->isProduction());
    }

### 3. Eloquent withCount(): Get Related Records Amount

    public function posts()
    {
    return $this->hasMany(Post::class);
    }
    
    public function comments()
    {
    return $this->hasManyThrough(Comment::class, Post::class);
    }

    public function index()
    {
    $users = User::withCount(['posts', 'comments'])->get();
    return view('users', compact('users'));
    }

Every parameter that is specified in withCount() method, becomes main object’s _count property. So in this case, we will have $user->posts_count and $user->comments_count variables.

Notice, that withCount() works with both hasMany() relationship, and also 2nd level deep with hasManyThrough().

Another example is that we can even filter the query with withCount() relationship. Let’s say that our comments table has a column approved, and then we can filter that separately and even assign an alias to that column name:

    $users = User::withCount([
    'posts',
    'comments',
    'comments as approved_comments_count' => function ($query) {
    $query->where('approved', 1);
    }])
    ->get();

And then we receive $user->approved_comments_count that we can use in Blade.

<a href="https://laravel.com/docs/8.x/eloquent-relationships#counting-related-models">Linc off.doc</a>
