# django-blog-cw1

Add edit blog post support to the blog project.


def post_edit(request, pk):
    post = get_object_or_404(Post, pk=pk)
    form = PostForm(request.POST, instance=post)
    if form.is_valid():
        post = form.save(commit=False)
        post.author = request.user
        post.published_date = timezone.now()
        post.save()
        print(pk)
        return redirect("post_detail", pk=post.pk)
    else:
        post = Post.objects.get(pk=pk)
        form = PostForm(instance=post)
        print(pk,'#2')
    return render(request,'blog_app/post_edit.html', {'form': form})
