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