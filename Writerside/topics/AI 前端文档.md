# AI 前端文档

<note>该文档介绍前端ai功能的页面以及模块，主要是为了实现模块以及代码的复用，并方便后期迭代修改。</note>
## 使用到的模块

### CollectTouch  
<note>用于收集埋点信息</note>
### ProfileDialogBox
<note>对话框组件，用于显示头像以及消息内容</note>

![profileDialogBox.png](profileDialogBox.png) 
<code-block>
参数:
export type Role = 'user' | 'assistant' | 'load' | 'system' | 'sending';
export interface Dialogue {
  role: Role;                                                               //用于分辨消息状态
  content: string;                                                          //消息内容
  profile: Source;                                                          //头像
  messageId?: string;                                                       //消息id
  hobby?: number;                                                           //用户喜好（点赞点踩）
  setLoading?: (value: ((prevState: boolean) => boolean) | boolean) => void;//加载回调
  onError?: (value: string) => void;                                        //报错回调
}
</code-block>  
### HobbyButton  
<note>点赞点踩组件</note> 

![HobbyButton.png](HobbyButton.png)
#### 参数
<code-block>    
interface HobbyProps {
  hobby: number;        //当前喜好
  onLike: () => void;   //当点赞时
  onDislike: () => void;//当点踩时
}
</code-block>
#### Api
<code-block>
export async function changeHobby(
  messageId: string,                //消息id
  hobby: Hobby,                     //修改后的喜好
  onError?: (value: string) => void,//报错回调
)
</code-block>
### HintAlert
<note>提醒弹窗组件</note>

![HintAlert.png](HintAlert.png)
### LoadingAlert
<note>加载弹窗组件</note>

![LoadingAlert.png](LoadingAlert.png)
## 难理解的代码结构
### 历史会话栏

![aiHistory-list.png](aiHistory-list.png)
<note>这里并不是做了个按日期分的组件，而是直接用列表，并判断每条会话是否为当天第一条或最后一条，然后分三种情况分配样式，模拟出上面的效果。好处就是不需要对列表进行后处理。</note>
<code-block>

        <ScrollView>
        {historyData.map((history, index) => (
          <View
            key={index}
            style={[
              styles.dateContain,
              {
                borderTopLeftRadius: isBegin(index) ? 24 : 0,
                borderTopRightRadius: isBegin(index) ? 24 : 0,
                marginTop: isBegin(index) ? 16 : 0,
                borderBottomLeftRadius: isEnd(index) ? 24 : 0,
                borderBottomRightRadius: isEnd(index) ? 24 : 0,
                marginBottom: isEnd(index) ? 16 : 0,
              },
            ]}
          >
            {isBegin(index) ? (
              <Text style={styles.dateText}>
                {getDateString(history.create_time)}
              </Text>
            ) : (
              <View
                style={{
                  width: '100%',
                  height: 1,
                  backgroundColor: 'rgba(0, 0, 0, 0.15)',
                  margin: -0.5,
                }}
              />
            )}
            <TouchableOpacity
              style={{
                flexDirection: 'row',
                alignItems: 'center',
                height: 48,
              }}
              onPress={() => {
                navigation.pop();
                navigation.replace('ai_chat', { sessId: history.session_id });
              }}
            >
              <Text
                style={styles.sessionTitle}
                numberOfLines={1}
                ellipsizeMode="tail"
              >
                {history.session_title +
                  (history.session_title.length < 20 ? '' : '...')}
              </Text>
              <Gap flex={1} />
              <Ionicons
                name={'chevron-forward'}
                size={24}
                color={'rgba(160, 124, 207, 0.5)'}
              />
              <Gap width={8} />
            </TouchableOpacity>
            {isEnd(index) && <Gap height={8} />}
          </View>
        ))}
      </ScrollView>
</code-block>

### 会话列表

![aiChat-list](aiChat-list.png)
<note>这里有很多问题，比如使用flatlist正序排列时，当新消息传入后列表不是在最下方，需要调用函数去拉到最底下。如果使用倒序排列，则默认会一直在最底下，
但是上拉加载用不了所以还是使用了正序排序，为了避免流式接收消息阻塞主线程，设置了每300ms更新一次消息。其中由于渲染后立刻调用scrollToEnd会无效，
因为flatlist高度更改的事件还没执行，所以很多地方在scrollToEnd外套了timeout。</note>
<code-block>

    <FlatList
        ref={scrollListRef}
        data={messageList}
        refreshControl={
          <RefreshControl refreshing={refreshing} onRefresh={onRefresh} />
        }
        keyExtractor={item => item.messageId}
        renderItem={({ item }) => (
          <ProfileDialogBox
            setLoading={setLoading}
            onError={onError}
            {...item}
          />
        )}
        style={styles.dialogContainer}
        keyboardShouldPersistTaps="never"
      />
</code-block>