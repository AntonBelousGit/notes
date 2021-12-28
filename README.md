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