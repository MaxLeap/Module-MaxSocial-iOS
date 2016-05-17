# Module-MaxSocial-iOS
##使用说明：

###一、设置appid和clientkey
1、在maxleap.cn中创建app，记录appid和clientkey。

2、更换AppDelegate.m中的宏定义为1中的appid和clientkey：

    #define MAXLEAP_APPID           @"your_app_id"
    #define MAXLEAP_CLIENTKEY       @"your_client_key"

3、如果要使用微博、QQ和微信第三方登录，需要先在相应的开发者后台注册app，输入正确的app信息。

4、更换AppDelegate.m中的以下宏定义：

    #define WECHAT_APPID            @"your_wechat_appid"
    #define WECHAT_SECRET           @"your_wechat_secret"
    #define WEIBO_APPKEY            @"your_weibo_appkey"
    #define WEIBO_REDIRECTURL       @"your_weibo_redirect_url"
    #define QQ_APPID                @"your_qq_appid"

5、更新Info.plist文件中URL Types中以上第三方登陆需要的设置。
###二、ViewController介绍
1、MCCreateNewPostViewController：发布说说界面，使用方法：

    MCCreateNewPostViewController *postViewController = [[MCCreateNewPostViewController alloc]init];
    [self.navigationController pushViewController:postViewController animated:YES];
 
2、MCTimelinePostsListViewController：说说界面，定义如下：

	
	@interface MCTimelinePostsListViewController : UIViewController
	
	// isSquare YES：表示广场，NO：其他
	@property (nonatomic, assign) BOOL isSquare;
	// isCycle YES：朋友圈 NO：timelineUser的发帖
	@property (nonatomic, assign) BOOL isCycle;
	// timelineUser未设置，则使用MaxLeapSignedUserId
	@property (nonatomic, strong) NSString *timelineUser;
	
	- (void)triggerPullToRefresh;
	- (void)hideCommentToolBarView;
	@end

启动广场界面代码如下：

	timeLinePostsVC = [[MCTimelinePostsListViewController alloc]init];
	timeLinePostsVC.isSquare = YES;
	timeLinePostsVC.hidesBottomBarWhenPushed = YES;
    [self.navigationController pushViewController:timeLinePostsVC animated:YES];
    
启动我的朋友圈界面代码如下：

	timeLinePostsVC = [[MCTimelinePostsListViewController alloc]init];
	timeLinePostsVC.isCycle = YES;
	timeLinePostsVC.hidesBottomBarWhenPushed = YES;
    [self.navigationController pushViewController:timeLinePostsVC animated:YES];
    
启动timelineUser的个人发布的说说界面代码如下：

	timeLinePostsVC = [[MCTimelinePostsListViewController alloc]init];
	timeLinePostsVC.hidesBottomBarWhenPushed = YES;
    [self.navigationController pushViewController:timeLinePostsVC animated:YES];
    
    
3、MCMomentsViewController：入口界面。