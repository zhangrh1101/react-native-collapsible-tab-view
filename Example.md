# React Native Collapsible Tab View

```tsx
import React from 'react'
import { View, StyleSheet, ListRenderItem } from 'react-native'
import { MaterialTabBar, MaterialTabItem, Tabs, useCurrentTabScrollY, useHeaderMeasurements } from 'react-native-collapsible-tab-view'

const HEADER_HEIGHT = 250

const DATA = [0, 1, 2, 3, 4]
const identity = (v: unknown): string => v + ''

const Header = () => {
  return <View style={styles.header} />
}

const Example: React.FC = () => {
  const renderItem: ListRenderItem<number> = React.useCallback(({ index }) => {
    return (
      <View style={[styles.box, index % 2 === 0 ? styles.boxB : styles.boxA]} />
    )
  }, [])
  
  const [headerHeight, setHeaderHeight] = useState();
    const headerOnLayout = useCallback((event: any) => {
        const { height } = event.nativeEvent.layout;
        console.log('setHeaderHeight', height)
        setHeaderHeight(height);
    }, []);

  
  const ScrollHeader = () => {
        // const { top, height } = useHeaderMeasurements()
        // const scrollY = useCurrentTabScrollY()
        // const scrollYText = useDerivedValue(() => {
        //     console.log('scrollYText', scrollY.value.toFixed(2));
        // })

        return (
            <View style={{ flex: 1 }} onLayout={headerOnLayout} >
                <StarContentView
                    style={{ backgroundColor: '#FFFFFF', borderRadius: 6 }}
                    isDetail={true}
                    index={tabIndex}
                    type={type}
                    wish={wish}
                    replyStyle={{ backgroundColor: '#F7F7F7' }}
                    textStyle={{ color: '#333333' }}
                    replyTextStyle={{ color: '#333333' }}
                />
                <View style={{ height: Theme.px2dp(16), backgroundColor: '#F4F8F9' }}></View>
            </View>
        );
    };
 
  const _renderScrollTabs = (props) => {
        let isTabActive = props.index.value == pageIndex
        return <View style={{ backgroundColor: '#FFFFFF', flexDirection: 'row', alignItems: 'center' }}>
            <MaterialTabBar
                {...props}
                style={{ paddingLeft: 5, height: Theme.px2dp(Theme.isIOS ? 80 : 80) }}
                activeColor={'#333333'}
                inactiveColor={'#666666'}
                labelStyle={{ fontSize: Theme.px2dp(26), fontWeight: '500' }}
                indicatorStyle={{ backgroundColor: '#53C7CB', borderRadius: 1.5, bottom: 6, width: 50 }}
                tabStyle={{ flexDirection: 'row', marginVertical: Theme.px2dp(0), paddingVertical: Theme.px2dp(10) }}
                scrollEnabled={true}
                isTabActive={isTabActive}
            />
            {/* 管理按钮 */}
            {/* <DynamicActionButton pageIndex={pageIndex} isMine={isMine} role={role} roleId={roleId} type={pageIndex} /> */}
        </View>
  }
    
  return (
    <View style={{ flex: 1, backgroundColor: '#FFFFFF' }}>

                    <Tabs.Container
                        ref={tabContainerRef}
                        lazy={true}
                        onTabChange={(value) => {
                            console.log('onTabChange', value.index);
                            setPageIndex(value.index);
                        }}
                        onIndexChange={(value) => {
                            console.log('onIndexChange', value);
                        }}
                        // headerHeight={headerHeight}
                        renderHeader={() => <ScrollHeader />}
                        renderTabBar={_renderScrollTabs}
                    >
                        < Tabs.Tab name="A" >
                            <DynamicsCommentsScreen tabLabel="A" isMine={true} />
                        </Tabs.Tab >

                        < Tabs.Tab name="B" >
                            <DynamicsCandlesScreen tabLabel="B" isMine={true} />
                        </Tabs.Tab >

                        < Tabs.Tab name="C" >
                            <DynamicsCandlesScreen tabLabel="C" isMine={true} />
                        </Tabs.Tab >

                    </Tabs.Container >
                </View>
  )
}

const styles = StyleSheet.create({
  box: {
    height: 250,
    width: '100%',
  },
  boxA: {
    backgroundColor: 'white',
  },
  boxB: {
    backgroundColor: '#D8D8D8',
  },
  header: {
    height: HEADER_HEIGHT,
    width: '100%',
    backgroundColor: '#2196f3',
  },
})

export default Example

```
